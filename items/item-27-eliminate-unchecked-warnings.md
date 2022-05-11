# Item 27: Eliminate Unchecked Warnings

## Main Takeaway

>Unchecked warnings are important. Don't ignore them. Every unchecked warning represents the potential for a `ClassCastException` at runtime. Do your best to eliminate these warnings. If you can't eliminate an unchecked warning and you can prove that the code that proved it is typesafe, suppress the warning with a `@SuppressWarnings("unchecked")` annotation in the narrowest possible scope. Record the rationale for your decision to suppress the warning as a comment.

## `@SuppressWarnings("unchecked")`

The `@SuppressWarnings` annotation will suppress any warnings at compile time, allowing only the user to reduce the amount of noise found in build logs. Adding `"unchecked"` can suppress unchecked cast warnings, unchecked method invocation warnings, unchecked parameterized vararg type warnings, and unchecked conversion warnings.

### How to use `@SuppressWarnings`

The `@SuppressWarnings` annotation can be used on any legal declaration, from an individual local variable to an entire class.

Always use the `@SuppressWarnings` annotation on the smallest scope possible (variable, method, or constructor). Never use `@SuppressWarnings` on an entire class.

Every time you use a `@SuppressWarnings` annotation, add a comment saying why it is safe to do so.

### Why `@SuppressWarnings` is important

If you ignore unchecked warnings that you know to be safe (instead of suppressing them), you won't notice when a new warning crops up that represents a real problem. The new warning will get lost amidst all the false alarms that you didn't silence.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-26-dont-use-raw-types.md)
- [Next](./item-27-eliminate-unchecked-warnings.md)
