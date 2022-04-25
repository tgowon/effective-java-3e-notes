# Item 1: Consider static factory methods instead of constructors

## Advantages

1. Unlike constructors, Static factory methods have names
2. Unlike constructors, they are not required to create a new object each time they’re invoked.
3. Unlike constructors, they can return an object of any subtype of their return type.
4. The class of the returned object can vary from call to call as a function of the input parameters.
5. The class of the retuned object need not exist when the class containing the method is written.

## Disadvantages

1. Classes without public or protected constructors cannot be subclassed
2. Static Factory Methods are hard to find
   1. They are not identified as factory methods via IDEs in the same way as Constructors; so users might not even know they are available for use.

Bloch also lists several naming conventions for SFMs that I can see in quite a few Google-related libraries that we use (he used to work at Google, so I’m not surprised).

**Service Provider Frameworks** are also a practical use-case for implementing SFMs.

> A service provider framework is a system in which providers implement a service, and the system makes the implementations available to clients, decoupling the clients from the implementations

### Service Provider Frameworks

(Taken from Stackoverflow)

> Consider something like the following:

```java
public interface MyService {
  void doSomething();
}

public class MyServiceFactory {
  public static MyService getService() {
    try {
      (MyService) Class.forName(System.getProperty("MyServiceImplemetation")).newInstance();
    } catch (Throwable t) {
      throw new Error(t);
    }
  }
}
```

> With this code, your library doesn’t need to know about the implementations of the service. Users of your library would have to set a system property containing the name of the implementation they want to use.
>
> This is what is meant by the sentence you don’t understand: the factory method will return an instance of some class (which name is stored in the system property "MyServiceImplementation"), but it has absolutely no idea what class it is. All it knows is that it implements MyService and that it must have a public, no-arg constructor (otherwise, the factory above will throw an Error).

## Navigation

- [All Items](../README.md#items)
- [Next](item-02.md)
