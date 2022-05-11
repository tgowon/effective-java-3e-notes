# Item 26: Don't use raw types

## Main Takeaway

> Using raw types can lead to exceptions at runtime, so don't use them. They are provided only for compatibility and interoperability with legacy code that predates the introduction of generics.
>
> **For Example - The `Set` class:**
>
> - `Set<Object>` is a parameterized type representing a set that can contain objects of any type
> - `Set<?>` is a wildcard type representing a set that contain only objects of some unknown type
> - `Set` is a raw type, which opts out of the generic type system.
>
> The first two are safe, the last is not.

## Generics - A Primer

### Generic Types

A class or interface whose declaration has one ore more type parameters is a generic class or interface. Collectively, they are known as **generic types**.

```java
List<E> //("list of E")
```

Each generic type defines a set of **parameterized types**, which consist of the class or interface name followed by an angle-bracketed list of **actual type parameters** corresponding to the generic type's formal type parameters.  

```java
List<String> //("list of string")

Map<String, Integer> // ("map of string to integer")
```

Each generic type defines a **raw type**, which is the name of the generic type used without any accompanying type parameters. Raw types behave as if all of the generic type information were erased from the type declaration. They exist primarily for compatibility with pre-generics (pre Java 5) code.

## Problems with raw types

When using raw types, you must explicitly class your objects used within your raw-type instance. If you accidentally pass in another type that doesn't correspond to your explicit casting, you will receive a `ClassCastException` at _runtime._

When types (for example, collections) are declared with parameterized declarations, if you erroneously insert the wrong class into a parameterized class, you will receive an error at _compile-time_.

> **NOTE:** It pays to discover errors as soon as possible after they are made, ideally at compile time.

If you use raw types, you lose all of the safety and expressiveness benefits of generics.

## Creating collections of arbitrary objects

`List<Object>` is a valid use-case for generics. It will allow the insertion of arbitrary objects. This is different from `raw types` because `List<Object>` explicitly told the compiler that it is capable of holding objects of any type, giving you type safety at compile time.

For example:

- passing `List<String>` to a `List` --> legal (but unsafe)
- passing `List<String>` to a `List<Object>` --> illegal (fails at compile time)

## The unbounded wildcard (?) type

If you want to use a generic type but you don't know or care what the actual type parameter is, use the _unbounded wildcard type_ `?`. It is capable of holding _any_ object.

```java
Set<?> //("set of some type")
```

### What is the difference between `Set<?>` and `Set`?

The wildcard type is safe and the raw type isn't. You can put any element into a collection with a raw type, easily corrupting the collection's type invariant; **you cannot put any element (other than null) into a `Collection<?>` without generating a compile-time error.**

## When are Raw Types useful?

### class literals

Class literals are only permitted to be raw types, array types, and primitive types:

```java
//Legal Class Literals
List.class, String[].class, int.class 

//Illegal Class Literals
List<String>.class, List<?>.class
```

### `instanceof` operator

It is illegal to use the `instanceof` operator on parameterized types other than unbounded wildcards.

The following is the preferred way to use the `instanceof` operator with generic types:

```java
//Legitimate use of raw type - instanceof operator
if(o instanceof Set){       // Raw type
    Set<?> s = (Set<?>) o;  // Wildcard type
}
```

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-25-limit-source-files-to-a-single-top-level-class.md)
- [Next](./item-27-eliminate-unchecked-warnings.md)
