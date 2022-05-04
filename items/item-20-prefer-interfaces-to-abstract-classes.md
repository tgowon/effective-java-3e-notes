# Item 20: Prefer interfaces to abstract classes

## Main Takeaway

>An interface is generally the best way to define a type that permits multiple implementations. If you export a nontrivial interface, you should strongly consider providing a skeletal implementation to go with it. To the extend possible, you should provide the skeletal implementation via default methods on the interface so that all implementors of the interface can make use of it. That said, restrictions on interfaces typically mandate that a skeletal implementation take the form of an abstract class.

## Why interfaces before abstract classes?

### Existing classes can be easily retrofitted to implement a new interface

To add a new interface, just use the `implementation` clause in your class declaration.

You cannot (easily) add a new abstract class to the class hierarchy because Java prohibits multiple inheritance. To get past this, one would have to potentially add an additional abstract class high up in the original class's hierarchy, which opens _all other classes_ to the API proposed within the newly added class, whether appropriate or not.

### Interfaces allow for the construction of non-hierarchial type frameworks

>The alternative is a bloated class hierarchy containing a separate class for every support combination of attributes. If there are `n` attributes, in the type system, there are 2<sup>n</sup> possible combinations that you might have to support. This is what's known as _combinatorial explosion_. Bloated class hierarchies can lead to bloated classes with many methods that differ only in the type of their arguments because there are no types in the class hierarchy to capture common behaviors.

### Interfaces enable safe, powerful functionality enhancements via "wrapper classes"

See ["Wrapper Classes" (Item 18).](item-18-favor-composition-over-inheritance.md#wrapper-classes-ie-the-decorator-pattern)

### Interfaces can be used as Mixins

A _mixin_ is a type that a class can implement in addition to its "primary type," to declare that it provides some optional behavior. For example `Comparable` is a mixin interface that allows a class to declare that its instances are ordered with respect to other mutually comparable objects. Such an interface is called a "mixin" because it allows the optional functionality to be "mixed in" to the type's primary functionality.

Abstract classes can't be used to define mixins because a class cannot have more than one parent.

## Designing Your API with Interfaces and Abstract Classes

### Start with Interfaces

Provide implementation assistance with `default` methods.

### Provide an `abstract` Skeletal Implementation class in addition to your Interface

Interfaces have several limitations

- Interfaces can specify the behavior, but not provide implementation (i.e. default methods), for `Object` methods such as `equals`, `hashCode`, and `toString`.
- Interfaces cannot contain instance fields or non-public static members

You can overcome these limitations by providing a "skeletal implementation class" in addition to the interface.

The interface defines the type (plus any default methods), and the skeletal implementation class implements the remaining non-primitive interface methods atop the primitive interface methods.

#### Skeletal Implementation Classes

Skeletal implementation classes are called `Abstract<Interface>` where `Interface` is the name of the interface they implement.

Skeletal implementation classes provide all of the implementation assistance of abstract classes without imposing the severe constraints that abstract classes impose when they serve as type definitions.

Users can choose to either extend the skeletal implementation class, or use the interface directly (and provide their own implementation of abstract methods).

Users can also forward invocations of interface methods to a contained instance of a private inner class that extends the skeletal implementation. This is known as "simulated multiple inheritance."

## Writing your API (pt 2)

>:warning: migrate to the "designing your interfaces/abstract classes section"

First, study the interface and decide which methods are the primitives in terms of which the others can be implemented. These primitives will be the abstract methods in your skeletal implementation. Next, provide default methods in the interface for all of the methods that can be implemented directly atop the primitives, but recall that you may not provide default methods for `Object`. If the primitives and default methods cover the interface, you're done, and have no need for a skeletal implementation class. Otherwise, write a class declared to implement the interface, with implementations of all the remaining interface methods. The class may contain any nonpublic fields and methods appropriate to the task.

Follow all of the [design and documentation](item-19-design-and-document-for-inheritance-or-else-prohibit-it.md) guidelines outlined in Item 19.

A minor variant on the skeletal implementation is the _simple implementation_: this is class is designed for inheritance but is not abstract.  It is the simplest possible working implementation.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-19-design-and-document-for-inheritance-or-else-prohibit-it.md)
- [Next](./item-20-prefer-interfaces-to-abstract-classes.md)
