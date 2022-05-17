# Item 30: Favor generic methods

## Main Takeaway

>Generic methods, like generic types, are safer and easier to use than methods required their clients to put explicit casts on input parameters and return values. Like types, you should make sure that your methods can be used without casts, which often means making them generic. And like types, you should generify existing methods whose use requires casts. This makes life easier for new users without breaking existing clients.

## Properties of Generic Methods

- Generic methods have a type parameter (the diamond operator enclosing the type) `before` the return type of the method declaration and _after_ the access modifiers (`public`, `private`, `static` etc.).
  - Example:
  
  ```java
  public <T> List<T> toList(T[] a)
  ```
  
  - This can be a list of types - conveniently called the _type parameter list_.
- Type parameters can be bounded.
- Generic methods can have different type parameters separated by commas in the method signature.
- The method body for a generic method is just like a normal method.

```java
//Example Generic Method
public <E> Set<E> union(Set<E> s1, Set<E> s2){
    Set<E> result = new HashSet<>(s1);
    result.addAll(s2);
    return result
}
```

## Generic Singleton Factory Pattern

This pattern is used when you need to create an object that is immutable but applicable to many different types. You can use a single object for all required type parameterizations, but you need to write a static factory method to repeatedly dole out the object for each requested type parameterization.

:warning: refer to the code example for this one (WIP)

## Recursive type bound (WIP)

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-29-favor-generic-types.md)
- [Next](./item-31-use-bounded-wildcards-to-increase-api-flexibility.md)
