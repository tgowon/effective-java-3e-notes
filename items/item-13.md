# Override `clone` judiciously

## Main Takeaway

> All classes that implement `Cloneable` should override `clone` with a public method whose return type is the class itself. This method should first call `super.clone`, then fix any fields that need fixing. Typically, this means copying any mutable objects that comprise the internal "deep structure" of the object and replacing the clone's references to these objects with references to their copies.
> 
> While these internal copies can usually be made by calling `clone` recursively, this is not always the best approach. If the class contains only primitive fields or references to immutable objects, then it is likely the case that no fields need to be fixed.
>
> Given all the problems associated with `Cloneable` **new interfaces should not extend it, and new extendable classes should not implement it.** While it's less harmful for final classes to implement `Cloneable`, this should be viewed as a performance optimization, reserved for the rare cases where its justified.
>
> Copy Functionality is best provided by [**\[copy\] constructors**](#copy-constructor) or [**\[copy\] factories**](#copy-factory).
>
> A notable exception to this rule is **arrays**, which are best copied with the `clone` method.

## `clone` can be problematic

## A Better Approach - Copy Constructors and Copy Factories

### Copy Constructor

```java
//Copy Constructor - take in a single argument of the same class type and create a new object.
public Foo(Foo foo){...}
```

### Copy Factory

```java
//Copy Factory - take in a single argument of the same class type and create a new object.
public static Foo newInstance(Foo foo){...}
```

### Rationale

- Copy Constructors/Factories do not rely on risk-prone a extralinguistic object creation mechanism
- they don't demand unenforceable adherence to thinly documented conventions
- they don't conflict with the proper use of final fields
- they don't throw unnecessary checked exceptions; and they don't require casts.

A Copy Constructor/Factory can take an argument whose type is an interface implemented by the class. For example:

```java
HashSet s = ...;
TreeSet ts = new TreeSet<>(s); //this is known as a conversion constructor
```

Copy Constructors/Factories (like the example above) with single-interface arguments that _convert_ objects to another type are known as **Conversion Constructors/Factories**.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-12.md)
- [Next](item-14.md)
