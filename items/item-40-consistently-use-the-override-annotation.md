# Item 40: Consistently use the Override annotation

## Main Takeaway

> The compiler can protect you from a great many errors if you see the `Override` annotation on every method declaration that you believe to override a supertype declaration, with one exception. In concrete classes, you need not annotate methods that you believe to override abstract method declarations (though it is not harmful to do so).

## Better takeaway

Use `Override` wherever possible, as you gain benefits from both the compiler (e.g. if you override a method inappropriately -- i.e. _overload_ rather than override), and/or the IDE (e.g. you intend to "override" a method that doesn't exist on the superclass). These annotations are not harmful to your program. In fact, they can improve code readability.

This includes abstract methods / interface methods (especially with the advent of default methods).

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-39-prefer-annotations-to-naming-patterns.md)
- [Next](./item-41-use-marker-interfaces-to-define-types.md)
