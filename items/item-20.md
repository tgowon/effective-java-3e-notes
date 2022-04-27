# Item 20: Prefer interfaces to abstract classes

## Main Takeaway

TBD

### Mixin Interfaces

A _mixin_ is a type that a class can implement in addition to its "primary type," to declare that it provides some optional behavior. For example `Comparable` is a mixin interface that allows a class to declare that its instances are ordered with respect to other mutually comparable objects. Such an interface is called a "mixin" because it allows the optional functionality to be "mixed in" to the type's primary functionality.

Abstract classes can't be used to define mixins because a class cannot have more than one parent.
