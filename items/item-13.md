# Override `clone` judiciously

## Main Takeaway

> All classes that implement `Cloneable` should override `clone` with a public method whose return type is the class itself. This method should first call `super.clone`, then fix any fields that need fixing. Typically, this means copying any mutable objects that comprise the internal "deep structure" of the object and replacing the clone's references to these objects with references to their copies.
>
> While these internal copies can usually be made by calling `clone` recursively, this is not always the best approach. If the class contains only primitive fields or references to immutable objects, then it is likely the case that no fields need to be fixed.

### When to use `clone`/`Cloneable`?

> Given all the problems associated with `Cloneable` **new interfaces should not extend it, and new extendable classes should not implement it.** While it's less harmful for final classes to implement `Cloneable`, this should be viewed as a performance optimization, reserved for the rare cases where its justified.
>
> Copy Functionality is best provided by [**\[copy\] constructors**](#copy-constructor) or [**\[copy\] factories**](#copy-factory).
>
> A notable exception to this rule is **arrays**, which are best copied with the `clone` method.

## `clone` / `Cloneable` - a Primer

Cloneable was intended to be a mixin interface (Item 20), but since it doesn't provide its own `clone()` method, it's not really one.

Instead, `Cloneable` determines the behavior of `Object`'s protected `clone` implementation: if a class implements `Cloneable`, `Object`'s `clone` method returns a field-by-field copy of the object; otherwise it throws `CloneNotSupportedException`.

This means if you implement `Cloneable`, _you must_ (...should) **override** the `clone` method on `Object` rather than _implement_ some method from `Cloneable`.

### What is `clone`?

`clone` is a native method found on the `Object` class. It satisfies the following criteria:

```java
x.clone() != x

x.clone.getClass() == x.getClass()
```

Note:

```java
x.clone().equals(x)
```

_can_ be `true`, but is not an absolute requirement.

Java's standard `clone` method follows **Shallow Copying** by default.

### Shallow Copy vs. Deep Copy

**Shallow Copying** is the method of copying an object where the fields of an old object `X` are copied to the new object `Y`. If the field value copied from `X` to `Y` is a _primitive type_, both objects will have the same primitive value.

**HOWEVER**, of a field copied from `X` to `Y` is a reference type, both `X` and `Y` will point to the **same reference**.

Therefore, **any changes made in referenced objects in object X or Y will be reflected in other objects**.

**Deep Copying** is similar Shallow Copying; however, in Deep Copying, all reference types from `X` and copied to `Y` such that `X` and `Y` **point to two different references whose values may be equal, but whose references are not the same.**

This can be accomplished by recursively/iteratively traversing reference types and calling `clone` (or copy) on their respective fields.

### When is `clone` useful?

#### Arrays

Using `object.clone()` for an array is the preferred idiom to duplicate an array.

Calling clone on an array returns an array whose runtime and compile-time types are identical to those of the array being cloned.

### Why is `clone`/`Cloneable` problematic?

1. The Cloneable architecture is incompatible with normal use of final fields referring to mutable objects. In order to make a class cloneable, it may be necessary to remove `final` modifiers from some fields.
2. A clone method should never invoke an overridable method on a clone under construction. If `clone` invokes a method that is overridden in a subclass, this method will execute before the subclass has had a change to fix its state in the clone, possibly leading to corruption in the `clone` and the original.
3. Clone needs to handle `CloneNotSupportedException`s because this is a checked exception on the `Object.java` method. This should have been unchecked, but it's not.
4. Programmers need to remember to check whether the overridden `clone` method need to be deep copied. Failure to do so can cause bugs / security holes.

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
