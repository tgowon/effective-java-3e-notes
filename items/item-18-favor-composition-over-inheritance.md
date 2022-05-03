# Item 18: Favor Composition over Inheritance

## Main Takeaway

>Inheritance is powerful, but it is problematic because it violates encapsulation. It is appropriate only when a genuine subtype relationship exists between the subclass and the superclass. Even then, inheritance mya lead to fragility if the subclass is in a different package from the superclass and the superclass is not designed for inheritance. To avoid this fragility, use composition and forwarding instead of inheritance, especially if an appropriate interface to implement a wrapper class exists. Not only are wrapper classes more robust than subclasses, they are also more powerful.

## Rationale

### Reliance on Implementation Details

Your subclass is obligated to stay up to date with the superclass it's extending. So, if the implementation details change on the superclass (due to a version change, etc.), the subclass may break, even though its own code hasn't been touched.

### New / Changed Functionality in the Superclass are Propagated Down

It is not a good idea to think it is safe to extend a class if you merely add new methods and refrain from overriding existing methods.

A superclass may take on new methods that expose the subclass to unintended security holes, as the client can bypass the subclass's checks by using methods on the superclass.

If the superclass acquires a new method with the same signature and a different return type, your subclass wil no longer compile. If you've given the subclass a method with the same signature and return type as the new superclass method, then you're now overriding it, and are subject to the problems described earlier. 

Futhermore, it is doubtful that your method will fulfill the contract of the new superclass method, because that contract had not yet been written when you wrote the subclass method.

## What is Composition

Composition -- Instead of extending an existing class, give your new class a private field that references and instance of the existing class.

Each instance method in the new class invokes the corresponding method on the contained instance of the existing class and returns the resulting. This is known as forwarding. ... The resulting class will have no dependencies on the implementation details of the existing class, and adding new methods to the existing class will have no impact on the new class.

### Wrapper Classes (i.e the Decorator Pattern)

SEE WRAPPER CLASS EXAMPLE

The example above is known as a wrapper class (i.e. the Decorator Pattern), because the new class "decorates" the existing class by adding additional behavior.

NOTE: This is sometimes referred to as _delegation_, but it is not technically delegation unless the wrapper object passes itself to the wrapped object.

#### Disadvantages

- Wrapper Classes are not suited for use in callback frameworks, wherein objects pass self-reference to other objects for subsequent invocations ("callbacks"). Because a wrapped object doesn't know of its wrapper, it passes a reference to itself (`this`), and callbacks elude the wrapper. This is known as the SELF problem. Some people worry about the performance impact of  forwarding method invocations or the memory footprint impact of wrapper objects. Neither turn out to have much impact in practice. It's tedious to write forwarding methods, but you have to write the reusable forwarding class for each interface only once, and forwarding classes may be provided for you.

## When to use Inheritance?

### Is `B` really an `A`?

If you cannot truthfully answer yes to this questions, B should not extend A. If the answer is no, it is often the case that B should contain a private instance of A and expose a different API: A is no an essential part of B, merely an implementation detail.

### Are you willing to expose implementation details?

If you use inheritance where composition is appropriate, you needlessly expose implementation details. The resulting API ties you to the original implementation forever, limiting the performance of your class. More seriously, by exposing the internals you let clients access them directly. This can lead to confusing semantics.

The client may also be able to corrupt invariants of the subclass by modifying the superclass directly.

Consider `Properties.java` for a list of problems exposed by extending `HashTable` instead of composing it.

### Are you willing to take on the flaws of the superclass in your new API?

Does the class you contemplate extending have any flaws in its API? If so, are you comfortable propagating those flaws into your class's API? Inheritance propagates any flaws in the superclass's API, while composition lets you design a new API that hides these flaws.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-17-minimize-mutability.md)
- [Next](item-19-design-and-document-for-inheritance-or-else-prohibit-it.md)
