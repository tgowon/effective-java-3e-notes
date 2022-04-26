# Item 11: Always override hashCode when you override equals

## Main Takeaway

> You _must_ override `hashCode` every time you override `equals` or your program will not run correctly. Your `hashCode` method must obey the general contract specified in `Object` and must do a reasonable job assigning unequal has codes to unequal instances.

## Rationale

Values return from `hashCode` must satisfy the following criteria:

- **When the `hashCode` method is invoked on an object repeatedly during an execution of an application, it must consistently return the same value, provide no information used in the `equals` comparisons is modified.** This value ned to remain consistent from one execution of an application to another.
- **If two objects are equal according to the `equals(Object)` method, then calling `hashCode` on the two objects must product the same integer result.**
- **If two objects are unequal according to the `equals(Object)` method, it is _not_ required that calling the hashCode on each of the objects must product distinct results.** However, the programmer should be aware that producing distinct results for unequal objects my improve the performance of hash tables.

Since equal objects must have equal hash codes, overriding `equals` requires overriding `hashCode` for the methods to remain consistent and in compliance.

## Pro-Tips: Designing a good  `hashCode` method

### Don't provide a detailed `hashCode` specification

> Don't provide a detailed specification for the value returned by `hashCode`, so clients can't reasonable depend on it; this gives you flexibility to change it.

If you leave the details unspecified and a flaw is found in the function or a better has function is discovered, you hvae change it in a subsequent release.

### When in doubt, let a machine do it for you

Modern IDEs, as well as Google's AutValue framework can generate a decent `hashCode` method.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-10.md)
- [Next](item-12.md)
