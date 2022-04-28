# Item 8: Avoid finalizers and cleaners

## Main Takeaway

> Don't use cleaners, or in releases prior to JDK 9, finalizers, except as a safety net or to terminate noncritical native resources. Even then, beware the indeterminacy and performance consequences.

- Finalizers are unpredictable, often dangerous, and generally unnecessary.
- Cleaners are less dangerous than finalizers, but still unpredictable, slow, and generally unnecessary.
- As a consequence, you should **never depend of a finalizer or cleaner to update persistent state.**

## What is a finalizer?

It is a **method** that the GC always calls just **before** the destroying an object. Once the `finalize` method completes, the GC immediately destroys that object.

### `finalize` syntax

```java
//Object.java
protected void finalize throws Throwable{} //it's empty
```

## A finalizer is not a (C++) destructor

- **The JVM's GC calls the finalizer** when it needs to reclaim storage associated with an object once it becomes unreachable.
- It's not expected that a program calls finalizers for its classes no longer in use.

In Java, to reclaim non-memory resources, using `try-with-resources` or `try-finally` blocks are normally used, and STRONGLY preferred.

## What about a Cleaner?

In **Java 9**, the `finalize()` method was  **deprecated** and a new **java.lang.ref.Cleaner** class was added to support garbage collection management. An object of **Cleaner** class gets notified automatically when an object becomes eligible for garbage collection. An object that is being garbage collected needs to be **registered with the cleaner object** by using the **register()** method.

### Basic `Cleaner` Example

```java
import java.lang.ref.Cleaner;
public class CleanerTest {
   public static void main(String args[]) {
      System.out.println("TutorialsPoint");
      Cleaner cleaner = Cleaner.create();
      if(true) {
         CleanerTest myObject = new CleanerTest();
            cleaner.register(myObject, new State());    // register cleaner
      }
      for(int i = 1; i <= 10000; i++) {
         String[] largeObject = new String[1000];
         try {
            Thread.sleep(1);
         } catch(InterruptedException e) {
              e.printStackTrace();
         }
      }
   }
   private static class State implements Runnable {
      public void run() {
         System.out.print("Cleaning action");
      }
   }
}
```

## Why Finalizers are Cleaners are best to be avoided

- GC decides when finalizers/cleaners are run.
  - **Major Takeaway:** Never do anything time-critical in a finalizer or a cleaner.
    - The promptness with which finalizers and cleaners are executed is primarily a function of the garbage collection algorithm, which varies widely across implementation.
- Exceptions can be hard to find
  - With finalizers, an uncaught exception thrown during finalization is ignored, and finalization of that object terminates. The user never is notified that a problem occurred.
- Finalizers have a serious security problem: they open your class up to finalizer attacks
  - (i.e. the finalizer of a malicious subclass can be run on a partially constructed object that should have "died" due to an error during Construction).
  - "Throwing an exception from a constructor should be sufficient to prevent an object from coming into existence; in the presence of finalizers, it is not.
    - **NOTE:** To protect non-final classes from finalizer attacks, write a final "finalize" method that does nothing.
- Cleaners are not much better than finalizers:
  - Class authors have control over their own cleaner threads, but cleaners still run in the background, under the control of the garbage collector, so there can be no guarantee of prompt cleaning.
    - There is no guarantee that the'll run at all. It is entirely possibly, even likely, that a program terminates without running them on some objects that are no longer reachable.
- There is severe performance penalty for using finalizers and cleaners.

## Legitimate Reasons to use finalizers and cleaners

- To act as a safety net in case the owner of a resource neglects to call its `close` method (assuming the resource implements `Closeable`/`AutoCloseable`).
- It manage resources with native peers.
  - A "native peer" is a native (non-Java) object to which a normal object delegates via native methods.
  - Because a native peer is not a normal object, the garbage collector doesn't know about it and can't reclaim it when its Java peer is reclaimed. This is where finalizer/cleaners come in handy.

## What should you do _instead_ of using finalizers / cleaners?

> Just have your class implement AutoCloseable, and require its clients to invoke the close method on each instance when it is no longer needed, typically using `try-with-resources` to ensure termination even in the face of exceptions (Item 9).
>
> One detail worth mentioning is that the instance must keep track of whether it has been closed: the `close` method must record in a field that the object is no longer valid, and other methods must check this field and throw an `IllegalStateException` if they are called after the object has been closed.

## An Example of a Cleaner / AutoCloseable in Action

```java
import java.lang.ref.Cleaner;  
  
//An autocloseable class using a cleaner as a safety net  
public class Room  implements AutoCloseable{  
    private static final Cleaner cleaner = Cleaner.create();  
  
    // Resource that requires cleaning. Must not refer to Room!  
    private static class State implements Runnable{  
        int numJunkPiles; // Number of junk piles in this room  
  
        State (int numJunkPiles){  
            this.numJunkPiles = numJunkPiles;  
        }  
  
        //Invoked by close method OR cleaner  
        @Override public void run(){  
            System.out.println("Cleaning room");  
            numJunkPiles = 0;  
        }  
    }  
  
  
    // The state of this room, shared with our cleanable  
    private final State state;  
  
    //Our cleanable. Cleans the room when it's eligibile for gc  
    private final Cleaner.Cleanable cleanable;  
  
    public Room(int numJunkPiles){  
        state = new State(numJunkPiles);  
        cleanable = cleaner.register(this,state);  
    }  
  
    @Override public void close(){  
        cleanable.clean();  
  
    }  
}  

```

### Called from Client Code

```java
//Cleaner called by AutoCloseable
class Adult{  
    public static void main(String[] args){  
        try(Room myRoom = new Room(7)){  
            System.out.println("Goodbye");  
        }  
    }  
}  

//Cleaner maybe called? Maybe not? All depends on the system running the program.
class Teenager{  
    public static void main(String[] args){  
        new Room(99);  
        System.out.println("Peace out");  
        // System.gc(); //no guarantee that after uncommenting this that the cleaner will clean  
    }  
}
```

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-07-eliminate-obsolete-object-references.md)
- [Next](./item-09-prefer-try-with-resources-to-try-finally.md)
