# Item 42: Prefer lambdas to anonymous classes

## Main Takeaway

> As of Java 8, lambdas are by far the best way to represent small function objects. Don't use anonymous classes for function objects unless you have to create instances of types that aren't functional interfaces. Also, remember that lambdas make it so easy to represent small function objects that it opens the door to functional programming techniques that were not previously practical in java.

## Function types / function objects / The Functional Interface

Interfaces with a single abstract method are _functional types_, and instances of their use are _functional objects_. As of Java 8, any interface with a single abstract method can now be denoted as a _functional interface_, and be used in lambda expressions.

## Lambda Expression Pro-tips

- **Omit the types of all lambda parameters** unless their presence makes your program clearer. If the compiler generates an error telling you it can't infer the type of a lambda parameter, then specify it.
- Lambdas lack names and documentation; **if a computation isn't self-explanatory, or exceeds a few lines, don't put it in a lambda** (use another construct like an anonymous class).
- **If a lambda is long or difficult to read, either find a way to simplify it or refactor your program to eliminate it.**
- **If you want to create an instance of an abstract class, you can do it with an anonymous class, but not a lambda.** You can use anonymous classes to create instances of interfaces with multiple abstract methods.
- **A lambda cannot obtain a reference to itself.** In a lambda, the `this` keyword refers to the enclosing instance, which is typically what you want. In an anonymous class, the `this` keyword refers to the anonymous class instance.
- **You should rarely, if ever, serialize a lambda** or anonymous class instance).

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-41-use-marker-interfaces-to-define-types.md)
- [Next](./item-42-prefer-lambdas-to-anonymous-classes.md)
