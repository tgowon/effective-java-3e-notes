# Item 29: Favor Generic Types

## Main Takeaway

>Generic types are safer and easier to use than types that require casts in client code. WHen you design new types, make sure that they can be used without such casts. This will often mean making the types generic. If you have any existing types that should be generic but aren't generify them. This will make life easier fro new users of these types without breaking existing clients.

## Converting to Generic Types

### 1. Add one or more type parameters to the class's declaration

#### Type Parameter Naming Conventions

Type parameters usually consist of a single letter. The following are the most commonly used parameter names:

- `T`: for an arbitrary type
  - Multiple type parameters are either denoted `T`, `U`, `V`, etc. or `T1`, `T2`, `T3`, etc.
- `E`: for the element type of a collection
- `K` and `V`: for the `key` and `value` types of a map
- `X`: for an exception
- `R`: for the return type of a function/method.

### 2. Replace all uses of the type `Object` (or your initial `type`) with the appropriate type parameter and then try to compile the resulting program

When attempting to write a generic type that is backed by an array, you can either make a single cast at the array's construction, or cast every operation on the array.

>The first is more readable: the array is declared to be of type E[], clearly indicating that it contains only `E` instances. It is also more concise: in an typical generic class, you read from the array at many points in the code; the first technique requires only a single cast (where the array is created), while the second requires a separate cast each time an array element is read. Thus the fist technique is preferable and more commonly used in practice.

## Pro Tips

### Use boxed primitive types instead of primitives

Using primitives in your generics will result in a compile-time error. This is a fundamental limitation of Java's generic type system. You can work around this restriction by using boxed primitive types.

### Use bounded type parameters where appropriate

This requires that the actual type parameter be a subtype of something you have explicitly listed.

```java
    class DelayQueue<E extends Delayed> implements BlockingQueue<E>
```

## Heap Pollution

Heap pollution occurs when a variable of a parameterized type refers to an object that is not of that type. It can cause the compiler's automatically generated casts to fail, violating the fundamental guarantee of the generic type system.

Note that heap pollution is not (generally) a concern when checking for type safety in your use for generic types backed by arrays in constructors.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-28-prefer-lists-to-arrays.md)
- [Next](./item-29-favor-generic-types.md)
