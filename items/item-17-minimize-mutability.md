# Item 17: Minimize Mutability

## Main Takeaway

> Resist the urge to write a setter for every getter. Classes should be immutable unless there's a very good reason to make them mutable. Immutable classes provide many advantages, and their only disadvantage is the potential for performance problems under certain circumstances. You should always make small [and oftentimes, large] value objects immutable. ... You should provide a public mutable companion class for your immutable class _only_ once you've confirmed that it's necessary to achieve satisfactory performance.
>
> If a class cannot be made immutable, limit its mutability as much as possible. ... Make every field final unless there's a compelling reason to make it non-final.... Declare every field `private` unless there's a good reason to do otherwise.
>
> Constructors should create fully initialized objects with all of their invariants established. Don't provide a public initialization method separate from the constructor or static factory unless there's a _compelling_ reason to do so. Don't provide a "reinitialize" method that enables an object to be reused as if it had be constructed with a different initial state.

## Immutable Classes

An immutable class is a class whose instances cannot be modified. All of the information contained in each instance is fixed for the lifetime of the object, so no changes can ever be observed.

1. Don't provide methods that modify the object's state (i.e. mutators -- `setFoo()`)
2. Ensure that the class can't be extended.
   1. Make the class `final`, or make the constructors `private`.
3. Make all fields final
4. Make all fields private
5. Ensure exclusive access to any mutable components
   1. If your class has any fields that refer to mutable objects, ensure that clients of the class cannot obtain references to these objects. Provide ["defensive copies"](item-50-make-defensive-copies-when-needed.md) if necessary.

## Immutability Favors the Functional Approach

:warning: Add code here

The Functional Approach: create and return a new value instance rather than modify the original instance. methods return the result of applying a function to their operand, without modifying it. 

Contrast to the procedural or imperative approach which methods apply a procedure to their operand, causing its state to change.

Note that the method names are prepositions(such as `plus`) rather than verbs (such as `add`). This emphasizes the fact that methods don't change the values of the objects.

## Immutability Notes

Immutable objects are simple. An immutable object can be in exactly one state, the state in which it was created. If you make sure that all constructors establish class invariants, then it is guaranteed that these invariants will remain true for all time, with no further effort of your part of the part of the programmer who uses the class. Mutable objects, on the other hand, can have arbitrarily complex state spaces. If eth documentation does not provide a precise description of the state transitions performed by mutator methods, it can be difficult or impossible to use a mutable class reliably.

Immutable objects are inherently thread-safe; they require no synchronization. They cannot be corrupted by multiple threads accessing them concurrently. This is far and away the easiest approach to achieve thread safety. Since no thread can ever observe any effect of another thread on an immutable object, immutable objects can be shared freely. Immutable classes should therefore encourage clients to reuse existing instances whenever possible. One easy way to do this is to provide public static final constants for commonly used values.

A consequence of the fact that immutable objects can be shared freely is that you never have to make _defensive copies_ of them. In fact, you never have to make any copies at all because the copies would be forever equivalent to the originals. Therefore, you need not and should not provide a `clone` method or `copy constructor` on an immutable class.

Not only can you share immutable objects, but they can share their internals.

Immutable objects make great building blocks for other objects, whether mutable or immutable. 

Immutable objects provide failure atomicity for free. Their state never chagnes, so there is no possibility of a temporary inconsistency.

Their major disadvantage is that they require a separate object for each distinct value; but you can provide a public mutable companion for situations where using only expensive, heavy immutable objects would become a performance concern (See `String` and `StringBuilder` -- not heavy, but for their complementary approaches)

Instead of making an immutable class final, you can make all of its constructors private or package-private and add public static factories in place of the public constructors.

Some immutable classes have one or more nonfinal fields in which they cache the results of expensive computations the fir time they are needed. If the same value is requested again, the cached value is returned, saving the cost of recalculation. this trick works precisely because the object is immutable, which guarantees that the computation would yield the same result if it were repeated.

Computing a value the first time its requested is called [lazy initialization](item-83).

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-16-in-public-classes-use-accessor-methods-not-public-fields.md)
- [Next](./item-17-minimize-mutability.md)
