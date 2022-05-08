# Item 24: Favor static member classes over nonstatic

## Main Takeaway

>There are four different kinds of nested classes: static member classes, nonstatic member classes, anonymous classes, and local classes.
>
>**Static/Nonstatic Member Classes:** If a nested class needs to be visible outside of a single method or is too long to fit comfortably inside a method, use a member class. If each instance of a member class needs a reference to its enclosing instance, make it nonstatic; otherwise, make it static.
>
>**Anonymous/Local Classes:** Assuming the class belongs inside a method, if you need to create instances from only one location and there is a preexisting type that characterizes the class, make it an anonymous class; otherwise, make it a local class.

## Static Member Classes

An ordinary class that happens to be declared inside another class and has access to all of the enclosing class's members, even those declared private.

Static member classes are useful as a public helper class in conjunction with its outer class. If its utility is beyond the scope of its outer class, make the static member class a top-level class on its own.

**Note:** If an instance of a nested class can exist in isolation from an instance of its enclosing class, then the nested class _must_ be a static member class: it is impossible to create an instance of a nonstatic member class without an enclosing instance.

## Nonstatic Member Classes

Similar to a static class except that it has a relation / necessity to exist along with an instance of its enclosing class. Each instance of the nested class will have a hidden reference to its enclosing class. This can take time an space, so be mindful when creating nested classes without the `static` keyword.

One common use of a nonstatic member class is to define an Adapter that allows an instance of the outer class to be viewed as an instance of some unrelated class.

### Beware - The cost of nonstatic member classes

Nonstatic member classes take time a space to hold a reference to its enclosing class. This can result in an [instance being retained when it would otherwise become eligible for garbage collection](./item-07-eliminate-obsolete-object-references.md).

## Anonymous Classes

An anonymous class is one without an enclosing class, that must be declared an instantiated simultaneously. Before lambdas were added to Java, anonymous classes were the preferred means of creating small function objects and process objects on the fly, but now lambdas are preferred.

Anonymous classes can also be used in the implementation of static factory methods, though lambda's _could_ be used in this use-case as well.

## Local Classes

Local classes can be declared practically anywhere a local variable can be declared, and will obey the same scoping rules. These are the least common nested classes. There are probably more optimal data structures useful as alternatives to local classes, but they are "legal" nonetheless.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-23-prefer-class-hierarchies-to-tagged-classes.md)
- [Next](./item-24-favor-static-member-classes-over-nonstatic.md)
