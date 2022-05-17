# Item 31: Use bounded wildcards to increase API flexibility

## Main Takeaway

>Using wildcard types in your APIs, while tricky, makes the APIs far more flexible. If you write a library that will be widely used, the proper use of wildcard types should be considered mandatory. Remember the basic rule: producer-`extends`, consumer-`super` (PECS). Also remember that all `comparable`s and `comparator`s are consumers.

## How to use

Use wildcard types on input parameters that represent producers or consumers

### PECS

**PECS** stands for **producer-`extends`, consumer-`super`**

If a parameterized type represents a `T` producer use `<? extends T>`; if it represents a `T` consumer, use `<? super T>`.

The PCES mnemonic captures the fundamental priciple that guides the use of wildcard types. Naftalin and Wadler call it the Get and Put Principle.

`Comparable`s and `Comparator`s are always consumers, so you should generally use `Comparable<? super T>` and `Comparator<? super T>`.

## Bounded wildcard return types

Do not use the bounded wildcard types as return types. This forces the wildcards to be required in client code.

If a user of a class has to think about wildcard types, there is probably something wrong with its API.

## Notes (WIP)

In a public API, if a type parameter appears only once in a method declaration, replace it with a wildcard.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-30-favor-generic-methods.md)
- [Next](./item-32-combine-generics-and-varargs-judiciously.md)
