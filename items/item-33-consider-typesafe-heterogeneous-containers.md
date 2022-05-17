# Item 33: Consider typesafe heterogeneous containers

## Main Takeaway

>The normal use of generics, exemplified by the Collections API, restricts you to a fixed number of type parameters per container. You can get around this restriction by placing the type parameter on the key rather than the container. You can use the `Class` objects as keys for such typesafe heterogeneous containers. A Class object used in this fashion is called a type token. You can also use a custom key type. For example, you could have a `DatabaseRow` type representing a database (the container), and a generic type `Column<T>` as its key.

## `Type` Tokens

When a class literal is passed among methods to communicate both compile-time and runtime type information, it is called a `type` token.

NOTE: The type of class literal is not simply `Class`, but `Class<T>`.

## The Typesafe Heterogeneous Container Pattern

A typesafe heterogeneous container instance is:

- typesafe: when it will never return an Integer when you ask it for a String.
- heterogenous: when all the keys in the collection can be of different types.

The implementation idea is to parameterize the key instead of the container.

### Why "Heterogeneous"?

All of the keys are a different within the container. This is unlike an ordinary map (container) where all the keys are the same.

## Dynamic casting

```java
public class `Class<T>` {
    T cast(Object obj);
}
```

The `cast` method is the dynamic analogue of Java's `cast` operator. It simply check that its argument is an instance of the type represented by the `Class` object (throwing `ClassCastException` if not possible).

## Class literals and generics

The class literal `List<String>.class` is a syntax error. This is because all `List<T>` classes share a single `Class` object, which is `List.class`.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-32-combine-generics-and-varargs-judiciously.md)
- [Next](./item-34-use-enums-instead-of-constants.md)
