# Item 38: Emulate extensible enums with interfaces

## Main Takeaway

> While you cannot write an extensible enum type, you can emulate it by writing an interface to accompany a basic enum type that implements the interface. This allows clients to write their own enums (or other types) that implement the interface. Instances of these types can then be used wherever instances of the basic enum type can be used, assuming APIs are written in terms of the interface.

## When are extensible enumerated types useful: `OpCodes`

"Operation Codes," or `opcodes` are enumerated types who elements represent operations on some machine. Sometimes it is desireable to let the users of an API provide their own operations effectively extending the set of `opcodes` provided by the API.

## Emulating extensible enumerated types: creating interfaces

Define an interface for the opcode type and an enum that is the standard implementation of the interface. While the standard implementation is not extensible, the interfaces methods would be; and the user is able to define another enum type that implements the same interface.

## Disadvantages

A minor disadvantage of the use of interfaces to emulate extensible enums is that implementations cannot be inherited from one enum type to another. If the implementation code does not rely on any state, it can be placed in the interface, using default implementations.  

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-37-use-enummap-instaed-of-ordinal-indexing.md)
- [Next](./item-38-emulate-extensible-enums-with-interfaces.md)
