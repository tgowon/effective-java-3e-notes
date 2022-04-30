# Item 15: Minimize the accessibility of classes and members

## Main Takeaway

> You should reduce accessibility of program elements as much as possible (within reason). After carefully designing a minimal public API, you should prevent any stray classes, interfaces, or members from becoming part of the API. With the exception of `public static final` fields, which serve as constants, public classes should have no public fields. Ensure that objects referenced by `public static final` fields are immutable.

## Rationale

>The single most important factor that distinguishes a well-designed component from a poorly designed on is the degree to which the component hides its internal data and other implementation details from other components.

- This is the essence of data encapsulation.

### Why Data Encapsulation Matters

- Components communicate only through their APIs and are oblivious to each others' inner workings
- Components are decoupled, allowing them to be developed, tested, optimized, used, understood, and modified in isolation.
- Increases software reuse because components that aren't tightly coupled often prove useful in other contexts besides the ones for which they were developed.
- Decreases the risk in building large systems because individual components may prove successful even in the system does not.

## Minimize Data Accessibility By Making Each Class or Member as Inaccessible as Possible

Use the lowest possible access level consistent with the proper functioning of the software that you are writing.

### Access Levels

- `private` - The member is accessible only from the top-level class where it is declared.
- _`package-private`_ - The member is accessible from any class in the package where it is declared. Technically known as the _default_ access, this is the access level you get if no modifier is specified (**except for interface members, which are public by default**)
- `protected` - The member is accessible from subclasses of the class where it is declared (subject to a few restrictions) and from any class in the package where it is declared.
- `public` - The member is accessible from anywhere.

### Overriding methods, and their Access Levels

If a method overrides a superclass method, it cannot have a more restrictive access level in the subclass than in the superclass. This is necessary to ensure that an instance of the subclass is usable anywhere that an instance of the superclass is usable.

**If you violate this rule** the compile will generate an error message when you try to compile the subclass (unless the class implements an interface: all public/ methods in an interface must be declared public in the class).

#### What about when testing?

>It is not acceptable to make a class, interface, or member a part of a package's exported API to facilitate testing

Either put your test in the tested-class's package, or update your class code to allow for an alternative means to test.

## General Takeaways

### Avoid `public` unless needed

Instance fields of public classes should rarely be public.

- Use accessor methods to access your fields, but keep the fields themselves private.
- Classes with public mutable fields are not generally thread-safe

`public static final` fields serving as constants are ok, as long as the objects referenced by `public static final` fields are immutable.

### Beware of public (static final) arrays

**A nonzero-length array is always mutable**, so it is wrong for a class to have a `public static final` array field or an accessor that returns such a field. If a class has such a field or accessor, clients wil be able to modify the contents of the array. This is a frequent source of security holes. For example:

```java
// Potential security hole!
public static final Thing[] VALUES == {...};
```

To resolve this, try one of the following solutions:

#### Add a public immutable list

```java
private static final Thing[] PRIVATE_VALUES = {...};
public static final List<Thing> VALUES = Collections.unmodifiableList(Arrays.asList(PRIVATE_VALUES));
```

#### Copy the private array

```java
private static final Thing[] PRIVATE_VALUES = {...};
public static final Thing[] values(){
    return PRIVATE_VALUES.clone();
}
```

NOTE: Remember that `.clone()` is the [preferred way to duplicate an array](./item-13-override-clone-judiciously.md).

## Modules Provide a Secondary Form of Data Encapsulation

As of JDK 9, the Java Module System can be used to group packages together by their (desired) level of accessibility, beyond what access levels are stated on the classes themselves. There are still ongoing discussions on how beneficial this is in practice.

>It is too early to say whether modules will achieve widespread use outside of the JDK itself. In the meantime, it seems best to avoid them unless you have a compelling need.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-14-consider-implementing-comparable)
- [Next](./item-16-in-public-classes-use-accessor-methods-not-public-fields.md)
