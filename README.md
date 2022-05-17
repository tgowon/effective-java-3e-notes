# Effective Java, 3rd Edition - Notes

This repo contains my notes from a read through of [_Effective Java, 3rd Edition_](https://www.pearson.com/us/higher-education/program/Bloch-Effective-Java-3rd-Edition/PGM1763855.html?) in 2022.

:warning: **This is a still a work in progress**! - Read at your own risk! :warning:

I'm currently reading an item a (work) day.

## Items

### Creating and Destroying Objects

- [Item 1: Consider static factory methods instead of constructors](items/item-01-consider-static-factory-methods-instead-of-constructors.md)
- [Item 2: Consider a builder when faced with many constructor parameters](items/item-02-consider-a-builder-when-faced-with-many-constructors.md)
- [Item 3: Enforce the singleton property with a private constructor or an enum type](items/item-03-enforce-the-singleton-property-with-a-private-constructor-or-an-enum-type.md)
- [Item 4: Enforce noninstantiability with a private constructor](items/item-04-enforce-non-instantiability-with-a-private-constructor.md)
- [Item 5: Prefer dependency injection to hardwiring resources](items/item-05-prefer-depdendency-injection-to-hardwiring-resources.md)
- [Item 6: Avoid creating unnecessary objects](items/item-06-avoid-creating-unnecessary-objects.md)
- [Item 7: Eliminate obsolete object references](items/item-07-eliminate-obsolete-object-references.md)
- [Item 8: Avoid finalizers and cleaners](items/item-08-avoid-finalizers-and-cleaners.md)
- [Item 9: Prefer `try`-with-resources to `try`-`finally`](items/item-09-prefer-try-with-resources-to-try-finally.md)

### Methods Common to All Objects

- [Item 10: Obey the general contract when overriding `equals`](items/item-10-obey-the-general-contract-when-overriding-equals.md)
- [Item 11: Always override `hashCode` when you override `equals`](items/item-11-always-override-hashcode-when-you-override-equals.md)
- [Item 12: Always override `toString`](items/item-12-always-override-tostring.md)
- [Item 13: Override `clone` judiciously](items/item-13-override-clone-judiciously.md)
- [Item 14: Consider implementing `Comparable`](items/item-14-consider-implementing-comparable.md)

### Classes and Interfaces

- [Item 15: Minimize the accessibility of classes and members](items/item-15-minimize-the-accessibility-of-classes-and-members.md)
- [Item 16: In public classes, use accessor methods, not public fields](items/item-16-in-public-classes-use-accessor-methods-not-public-fields.md)
- [Item 17: Minimize mutability](items/item-17-minimize-mutability.md)
- [Item 18: Favor composition over inheritance](items/item-18-favor-composition-over-inheritance.md)
- [Item 19: Design and document for inheritance or else prohibit it](items/item-19-design-and-document-for-inheritance-or-else-prohibit-it.md)
- [Item 20: Prefer interfaces to abstract classes](items/item-20-prefer-interfaces-to-abstract-classes.md)
- [Item 21: Design interfaces for posterity](items/item-21-design-interfaces-for-posterity.md)
- [Item 22: Use interfaces only to define types](items/item-22-use-interfaces-only-to-define-types.md)
- [Item 23: Prefer class hierarchies to tagged classes](items/item-23-prefer-class-hierarchies-to-tagged-classes.md)
- [Item 24: Favor static member classes over nonstatic](items/item-24-favor-static-member-classes-over-nonstatic.md)
- [Item 25: Limit source files to a single top-level class](items/item-25-limit-source-files-to-a-single-top-level-class.md)

### Generics

- [Item 26: Don’t use raw types](items/item-26-dont-use-raw-types.md)
- [Item 27: Eliminate unchecked warnings](items/item-27-eliminate-unchecked-warnings.md)
- [Item 28: Prefer lists to arrays](items/item-28-prefer-lists-to-arrays.md)
- [Item 29: Favor generic types](items/item-29-favor-generic-types.md)
- [Item 30: Favor generic methods](items/item-30-favor-generic-methods.md)
- [Item 31: Use bounded wildcards to increase API flexibility](items/item-31-use-bounded-wildcards-to-increase-api-flexibility.md)
- [Item 32: Combine generics and varargs judiciously](items/item-32-combine-generics-and-varargs-judiciously.md)
- [Item 33: Consider typesafe heterogeneous containers](items/item-33-consider-typesafe-heterogeneous-containers.md)

### Enums and Annotations

- Item 34: Use enums instead of int constants
- Item 35: Use instance fields instead of ordinals
- Item 36: Use EnumSet instead of bit fields
- Item 37: Use EnumMap instead of ordinal indexing
- Item 38: Emulate extensible enums with interfaces
- Item 39: Prefer annotations to naming patterns
- Item 40: Consistently use the Override annotation
- Item 41: Use marker interfaces to define types

### Lambdas and Streams

- Item 42: Prefer lambdas to anonymous classes
- Item 43: Prefer method references to lambdas
- Item 44: Favor the use of standard functional interfaces
- Item 45: Use streams judiciously
- Item 46: Prefer side-effect-free functions in streams
- Item 47: Prefer Collection to Stream as a return type
- Item 48: Use caution when making streams parallel

### Methods

- Item 49: Check parameters for validity
- Item 50: Make defensive copies when needed
- Item 51: Design method signatures carefully
- Item 52: Use overloading judiciously
- Item 53: Use varargs judiciously
- Item 54: Return empty collections or arrays, not nulls
- Item 55: Return optionals judiciously
- Item 56: Write doc comments for all exposed API elements

### General Programming

- Item 57: Minimize the scope of local variables
- Item 58: Prefer for-each loops to traditional for loops
- Item 59: Know and use the libraries
- Item 60: Avoid float and double if exact answers are required
- Item 61: Prefer primitive types to boxed primitives
- Item 62: Avoid strings where other types are more appropriate
- Item 63: Beware the performance of string concatenation
- Item 64: Refer to objects by their interfaces
- Item 65: Prefer interfaces to reflection
- Item 66: Use native methods judiciously
- Item 67: Optimize judiciously
- Item 68: Adhere to generally accepted naming conventions

### Exceptions

- Item 69: Use exceptions only for exceptional conditions
- Item 70: Use checked exceptions for recoverable conditions and runtime exceptions for programming errors
- Item 71: Avoid unnecessary use of checked exceptions
- Item 72: Favor the use of standard exceptions
- Item 73: Throw exceptions appropriate to the abstraction
- Item 74: Document all exceptions thrown by each method
- Item 75: Include failure-capture information in detail messages
- Item 76: Strive for failure atomicity
- Item 77: Don’t ignore exceptions

### Concurrency

- Item 78: Synchronize access to shared mutable data
- Item 79: Avoid excessive synchronization
- Item 80: Prefer executors, tasks, and streams to threads
- Item 81: Prefer concurrency utilities to wait and notify
- Item 82: Document thread safety
- Item 83: Use lazy initialization judiciously
- Item 84: Don’t depend on the thread scheduler

### Serialization

- Item 85: Prefer alternatives to Java serialization
- Item 86: Implement Serializable with great caution
- Item 87: Consider using a custom serialized form
- Item 88: Write readObject methods defensively
- Item 89: For instance control, prefer enum types to readResolve
- Item 90: Consider serialization proxies instead of serialized instances

## Resources

- Buy the book! Support the Author! [_Effective Java, 3rd Edition_](https://www.pearson.com/us/higher-education/program/Bloch-Effective-Java-3rd-Edition/PGM1763855.html?)
- [Github: Official Source Code for _Effective Java, 3e_](https://github.com/jbloch/effective-java-3e-source-code)
- [Google Docs: Official Errata for _Effective Java, 3e_](https://docs.google.com/document/d/1mAeEgQu4H4ADxa03k7YaVDjIP5vJBvjVIjg3DIvoc8E/edit)
- [Oracle Interview: "More Effective Java With Google's Joshua Bloch"](https://www.oracle.com/technical-resources/articles/javase/bloch-effective-08-qa.html)
- [Dev.to: Kyle Carter's "Effective Java Tuesday!" Series](https://dev.to/kylec32/effective-java-tuesday-let-s-consider-static-factory-methods-170p)
