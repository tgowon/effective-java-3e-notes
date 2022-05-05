# Item 21: Design interfaces for posterity

## Main Takeaway

>Default methods are extremely useful for providing standard method implementations when an interface is created, to ease the task of implementing the interface.
>
> [...However...]
>
> Using default methods to add new methods to existing interfaces should be avoided unless the need is critical.

## Rationale

### Default methods inject new logic to existing classes

The declaration for a default method includes a default implementation that is used by all classes that implement the interface but do not implement the default method.

[When adding to an existing interface] default methods are "injected" into existing implementations without the knowledge or consent of their implementers.

It is not always possible to write a default method that maintains all invariants of every conceivable implementation. As a result, existing implementations of an interface may compile without error or warning but fail at runtime.

### Default methods can only provide additional logic, not change/remove existing behavior

Default methods were not designed to support removing methods from interfaces or changing the signatures of existing methods. Neither of these interface changes is possible without breaking existing clients.

## Pro-tip: Test before you release your interfaces

At minimum, you should aim for three diverse implementations. Write multiple client programs that use instances of each new interface to perform various tasks.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-20-prefer-interfaces-to-abstract-classes.md)
- [Next](./item-21-design-interfaces-for-posterity.md)
