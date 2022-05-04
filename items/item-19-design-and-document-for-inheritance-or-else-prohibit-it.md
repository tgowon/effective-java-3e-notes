# Item 19: Design and document for inheritance or else prohibit it

## Main Takeaway

> **[When designing a class for inheritance]** you must document all of its self-use patterns, and once you've documented them, you must commit to them for the life of the class. If you fail to do this, subclasses may become dependent on implementation details of the superclass and may break if the implementation of the superclass changes.
>
> To allow others to write _efficient_ subclasses, you may have to export one or more `protected` methods.
>
> Unless you know there is a real need for subclasses, you are probably better off prohibiting inheritance by declaring your class `final` or ensuring that there are no accessible constructors.

## Rationale - The need for proper documentation

Programmers need to know what the ramifications of overriding methods that can change the behavior of superclasses. Without proper documentation, it is possible that an overridden method can unintentionally affect the the inner workings of an unrelated method in the inherited class.

To avoid this problem, the superclass must document its self-use of overridable methods, usually in an **"Implementation Requirements"** section of the method's **javadoc**.

**NOTE:** This type of documentation violates the dictum that good **API documentation should describe _what_ a given method does and not _how_ it does it.** This is a consequence of the fact that **inheritance violates encapsulation.**

To document a class so that it can be safely subclassed, you must describe implementation details that should otherwise be left unspecified.

## `protected` - Another (potential) necessity with inheritance

To allow programmers to write efficient subclasses without undue pain, a class may have to provide hooks into its internal workings in the form of judiciously chosen `protected` methods.

### Which methods should be `protected`?

You should expose as few protected members as possible because each one represents a commitment to an implementation detail.

The only way to test a class designed for inheritance is to write subclasses. This will show you whether a certain method needs its access level changed (`protected` if needed, `private` if never used).

Experience shows that three subclasses are usually sufficient to test an extendable class. You must test your class by writing subclasses _before_ you release it.

## You've allowed for overridable methods. Now what?

**Constructors must not invoke overridable methods, directly or indirectly.** If you violate this rule, program failure will result.

### Why?

The superclass constructor runs before the subclass constructor, so the overriding method in the subclass will get invoked before the subclass constructor has run. If the overriding method depends on any initialization performed by the subclass constructor, the method will not behave as expected.

SEE EXAMPLE -- `Super()` vs `Sub()`

**NOTE:** It is safe to invoke private methods, final methods, and static methods in a constructor, as none of them are overridable.

### `Cloneable` and `Serializable` - Things to Avoid

If you decide to implement either Cloneable or Serializable in a class that is designed for inheritance, you should be aware that because clone and readObject methods behave a lot like constructors, a similar restriction applies: neither clone nor readObject may invoke an overridable method, directly or indirectly.

## What should you do when inheritance is necessary?

There are some situations where designing for inheritance is the right thing to do, such as abstract classes, including skeletal implementations of interfaces (Item 20).

### Avoid self-use overridable classes

Eliminate the class's self-use of overridable methods entirely. In doing so, you'll create a class that is reasonably safe to subclass. Overriding a method will never affect the behavior of any other method.

#### Create `private` helper methods

Move the body of each overridable method to a private "helper method" and have each overridable method invoke its private helper method. Then replace each self- use of an overridable method invoke its private helper method. Then replace each self-use of an overridable method with a direct invocation of the overridable method's private helper method.

## Inheritance Alternatives

### Prefer interface design over pure inheritance

If a class implements some interface that captures its essence, such as `Set`, `List`, or `Map`, then you should feel compunction about prohibiting subclassing. The _wrapper class_ pattern, described in Item 18, provides a superior alternative to inheritance for augmenting the functionality.

### Best solution - prohibit subclassing entirely

There are two ways to prohibit subclassing. The easier of the two is to declare the class final .The alternative is to make all the constructors private or package-private and to add public static factories in place of the constructors. This alternative provides the flexibility to use subclasses internally

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-18-favor-composition-over-inheritance.md)
- [Next](./item-20-prefer-interfaces-to-abstract-classes.md)
