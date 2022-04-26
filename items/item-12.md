# Item 12: Always Override `toString`

## Main Takeaway

> Override `Object`s `toString` implementation in every instantiable class you write, unless a superclass has already done so. It makes classes much more pleasant to use and aids in debugging. The `toString` method should return a concise, useful description of the object, in an aesthetically pleasing format.

## Rationale

Providing a good `toString` implementation makes your class much more pleasant to use and makes systems using the class easier to debug.

## Pro-Tips: Designing a good `toString` method

### Make it human-readable

Java already provides a default `toString` method on every class, but the format consists of the `className` followed by `@` and the unsigned hex representation of the instances `hashCode`.  

`"IceCream@163b91"` is less readable than `"[IceCream: flavor=vanilla, size=small, container=Waffle Cone]"`

### Provide the interesting bits

When practical, the `toString` method should return _all_ of the interesting information contained in the object. This should make it easy for the user.

### Provide useful accessors

Provide programmatic access to the infomration contained in the value returned by `toString`.

- e.g. for `"[IceCream: flavor=vanilla, size=small, container=Waffle Cone]"`, the following accessors should also exist:
  - `getFlavor()`
  - `getSize()`
  - `getContainer()`

### Don't make the user parse `toString()` to get useful info

Do not include any data in the returned string that otherwise could not be acesssed programmatically.

- e.g. do not provide "toppings=sprinkles" if a `getToppings()` accessor does not exist.

By failing to provide accessors, you turn the `toString` format into a de facto API, even if you've specifed that it's subject to change.

### Avoid writing `toString` methods on Static Utility classes and `Enum` classes

- `Static Utiltiy` classes shouldn't have any associated value requiring string representation
- Java provides a good, built-in string representation for the `Enum` class.

### Write a `toString` method in any abstract class whose subclasses share a common string representation

For example, see the `toString` implementation in Java's abstract collection classes.>

### When in doubt, let a machine do it for you

Modern IDEs, as well as Google's AutValue framework can generate a decent `toString()` method.

## Should I document the return value format for `toString`?

### Advantages

> The advantage of specifying the format is that it serves as a standard, unambiguous, human readable representation of teh object. This representation can be used for input and output and in persistent human-readable data objects (e.g. CSV, JSON, etc.).

#### Pro-Tip: Construct instances from `toString` values

> If you specify the format, it's usually a good idea to provide a matching static factory or constructor so programmers can easily translate back and forth between the object and its string representation.

### Disadvantages

> The disadvantage of specifying the format of the `toString` return value is that once you've specified it, you're stuck with it for life, assuming your class is widely used.

### Takeaway

> Whether or not you decide to specify the format, you should clearly document your changes.

Either document _precisely_ what format the class will use, or state that the representation is subject to change. eg.

```java
/**
* Returns a brief description of IceCream. The exact details of this representation are
* unspecified and subject to change, but the following may be regarded as typical:
*
* "[IceCream: flavor=vanilla, size=small, container=Container.WAFFLE_CONE]"
*/
```

## Navigation

- [All Items](../README.md#items)
- [Previous](item-11.md)
- [Next](item-13.md)
