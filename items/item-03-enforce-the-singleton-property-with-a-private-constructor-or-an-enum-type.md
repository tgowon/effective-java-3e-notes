# Item 3: Enforce the singleton property with a private constructor or an enum type

## Main takeaway  

> The single-element enum type is often the best way to implement a singleton.

## Rationale

This is because a single-element enum provides the following advantages:  

1. Is more concise (than the `public static final INSTANCE` field approach)
2. Provides serialization functionality for free (i.e. use the native serialization built into enum types instead of worrying about setting up your own _Java_ serialization (…not exactly sure why you’d use Java serialization at this point, though…)
3. Provides guarantee against multiple instantiation.

Not that you cannot use this approach if your singleton needs to extend a superclass other than Enum — though you can get away with this if your “superclass” logic lives in an interface (and remember that interfaces can have both public AND private [as of JDK 9] `default` methods )

Bloch also writes about when the static factory approach for Singletons are useful.  

1. If you use a SFM for a singleton (i.e. `FOO.getInstance()`), you can change the implementation of the API without change changing the API itself.
   1. For example, your SFM can start creating new instances per thread rather than always returning the same instance. From the API client’s perspective there is no contract change.
2. SFMs can be used for a Generic Singleton Factory — but I have no idea what that is yet (that’s Item 30).
3. SFMs can be used as suppliers in method references (e.g. `Foo::instance` is a `Supplier<Foo>`)

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-03-enforce-the-singleton-property-with-a-private-constructor-or-an-enum-type.md)
- [Next](./item-04-enforce-non-instantiability-with-a-private-constructor.md)
