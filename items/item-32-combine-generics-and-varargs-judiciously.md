# Item 32: Combine generics and varargs judiciously

## Main Takeaway

>Varargs and generics do not interact well because the varargs facility is a leaky abstraction built atop arrays, and arrays have different type rules from generics. Though generic varargs parameters are not typesafe, they are legal. If you choose to write a method with a generic (or parameterized) varargs parameter, first ensure that the method is typesafe, and then annotate it with `@SafeVarargs` so it is not unpleasant to use.

## Heap Pollution

Heap pollution occurs when a variable of a parameterized type refers to an object that is not of that type. It can cause the compiler's automatically generated casts to fail, violating the fundamental guarantee of the generic type system.

## `@SaveVarargs`

The `@SaveVarargs` annotation lets the user know that the method's varargs parameters are typesafe.

### Ensuring typesafety

1. If the method doesn't store anything into the varargs array, then it's safe.
2. If the method doesn't make the array (or clone) visible to untrusted code.
3. If the varargs parameter array is used only to transmit a variable number of arguments from the caller to the method, then it's safe.

### Usage

Use `@SaveVarargs` on every method with a varargs parameter of a generic or parameterized type. This implies that you should _never_ write unsafe varargs methods. Every time the compiler warns you of possible heap pollution

The `@SaveVarargs` annotation is legal on static methods, final instance methods, and private instance methods.

### Exceptions

It is safe to pass the varargs array to another varargs methods that is correctly annotated with `@SaveVarargs`.

It is also safe to pass the array to a non-varargs method that merely computers some function of the contents of the array.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-31-use-bounded-wildcards-to-increase-api-flexibility.md)
- [Next](./item-33-consider-typesafe-heterogeneous-containers.md)
