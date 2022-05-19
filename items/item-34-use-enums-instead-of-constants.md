# Item 34: Use enums instead of `int` constants

## Main Takeaway

> The advantages of enum types over `int` constants are compelling. Enums are more readable, safer, and more powerful. Many enums require no explicit constructors or members, but others benefit from associating data with each constant and providing methods whose behavior is affected by this data. Fewer enums benefit from associating multiple behaviors with a single method. In this relatively rare case, prefer constant-specific methods to enums that switch on their own values. Consider the strategy enum pattern if some, but not all, enum constant share common behaviors.

## Enums - a primer

An "enumerated type" is a type whose legal values consist of a fixed set of constants, such as the seasons of the year, the planets in the solar system, or the suits in the deck of playing cards.

The basic idea behind Java's enum types is simple: they are classes that export one instance for each enumeration constant via a public static final field. Enum types are effectively final, by virtual of having no accessible constructors. Because clients can neither create instances of an enum type nor extend it, there can be no instances but the declared enum constants.

To associated data with enum constants, declare instance fields and write a constructor that takes the data and stores it in the fields. Enums are by their nature immutable, so all fields should be final. Fields can be public, but it's better to make them private and provide public accessors.

Enums have a static `values()` method that returns an array of its values in the order they were declared. Note also that the `toString` method returns the declared name of each enum value, enabling easy printing.

Just as with other classes, unless you have a compelling reason to expose an enum method to its clients, declare it private or (if need be) package-private.

If an enum is generally useful, it should be a top-level class; if its use is tied to a specific top-level class, it should be a member class of that top-level class.

Enum types have an automatically generated `valueOf(String)` method that translates a constant's name into the constant itself. If you override the `toString` method in an enum type, consider writing a `fromString` method to translate the custom string representation back to the corresponding `enum`.

Enum constructors aren't permitted to access the enum's static fields, with the exception of constant variables. This restriction is necessary because static fields have not yet been initialized when enum constructors run. A specif case of this restriction is that enum constants cannot access one another from their constructors.

Use enums any time you need a set of constants whose members are known at compile time. It is not necessary that the set of constants in an enum type stay fixed for all time.

A minor performance disadvantage is that there is a time/space cost to load an initialize enum types, but it is unlikely to be noticeable in practice.

## Should I use `switch` statements?

It depends.

(:warning: Add code example here)

This won't compile without the `throw` statement because the end of the method is technically reachable, even though it will never be reached.

There is a better way to associate a different behavior with each enum constant: declare an abstract apply method in the enum type, and override it with a concrete method for each constant in a "constant-specific class body." Such methods are known as "constant-specific method implementations."

(:warning: show CSMI example here)

Note that switch statements can also be dangerous from a maintenance perspective.

### When to use `switch` statements?

Switches are on enums are good for augmenting enum types with constant-specific behavior.

## Why is the  "`int` enum pattern" problematic?

```java
public static final int PLANET_MERCURY = 0;
public static final int PLANET_VENUS = 1;
public static final int PLANET_EARTH = 2;
public static final int PLANET_MARS = 3;
```

This provides nothing in the way of type safety and little in the way of expressive power.

There is no easy way to translate `int` enum constants into printable strings.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-33-consider-typesafe-heterogeneous-containers.md)
- [Next](./item-35-use-instance-fields-instead-of-ordinals.md)
