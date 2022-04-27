# Item 7: Eliminate Obsolete Object References

## Main Takeaway

An obsolete reference is a reference that will never be dereferenced again. If an object reference is unintentionally retained (i.e. becomes "obsolete" from the perspective of the program), not only is that object excluded from garbage collection, but  any objects referenced by that object (and their own references, etc.) are also excluded from GC.  

## Example - Insidious Obsolete References from a simple Stack

In the example below, the Stack class has a memory leak because if the stack grows and then shrinks, the objects that were popped off the stack will not be garbage collected, even if the program using the stack has no more references to them. In this case, the "obsolete references" are any elements that are outside the "active portion" of the stack array (i.e. any elements that have an index greater than `size`).

```java
// Can you spot the "memory leak"?
public class Stack {
 private Object[] elements;
 private int size = 0;
 private static final int DEFAULT_INITIAL_CAPACITY = 16;
 public Stack() {
  elements = new Object[DEFAULT_INITIAL_CAPACITY];
 }
 public void push(Object e) {
  ensureCapacity();
  elements[size++] = e;
 }
 public Object pop() {
  if (size == 0)
   throw new EmptyStackException();
  return elements[--size];
 }

/**
* Ensure space for at least one more element, roughly
* doubling the capacity each time the array needs to grow.
*/
 private void ensureCapacity() {
  if (elements.length == size)
   elements = Arrays.copyOf(elements, 2 * size + 1);
 }
}
```

To resolve this case, you call null out references once they become obsolete:

```java
public Object pop() {
 if (size == 0){
  throw new EmptyStackException();
 }
 Object result = elements[--size];
 elements[size] = null; // Eliminate obsolete reference
 return result;
}
```

### Nulling out object references should be the exception rather than the norm

The best way to eliminate an obsolete reference is to let the variable fall out of scope (which happens naturally if you define each variable in its narrowest possible scope [Item 57]).

**In general:** whenever a class manages its own memory, you should be alert for memory leaks, and identify whenever references should be nulled out when no longer in use.

### Other instances for common memory leaks

- caches -- it's easy to forget that an item is in a cache, and leave it in the cache long after it becomes irrelevant.
  - You can resolve this by using a `WeakHashMap`, which automatically removes entries when they become obsolete.
  - You can use a background thread to check whether items in the cache are still useful, or if their TTL has expired (assuming you've included one).
- listeners and other callbacks -- if you implement and API where clients register callbacks but don't deregister them explicitly, they will accumulate.
  - Resolve this by storying only "weak references" to them.

**Question:** What is a "weak reference"? See supported doc (TBD)

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-06-avoid-creating-unnecessary-objects.md)
- [Next](./item-08-avoid-finalizers-and-cleaners.md)
