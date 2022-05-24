# Item 36: Use `EnumSet` instead of bit fields

## Main Takeaway

> Just because an enumerated type will be used in sets, there is no reason to represent it with bit fields. The `EnumSet` class combines the conciseness and performance of bit fields with all the many advantages of enum types described in Item 34. The one real disadvantage of `EnumSet` is that it is not, as of Java 9, possible to create an immutable `EnumSet`, but this will likely be remediated in an upcoming release. In the meantime, you can wrap an `EnumSet` with Collections.`unmodifiableSet`, but conciseness and performance will suffer.

## What is a bit field?

A bit field is a data structure that consists of one or more adjacent bits which have been allocated for specific purposes, so that any single bit or group of bits within the structure can be set or inspected.

```java
public class Text{
    public static final int STYLE_BOLD          = 1 << 0; // 1
    public static final int STYLE_ITALIC        = 1 << 1; // 2
    public static final int STYLE_UNDERLINE     = 1 << 2; // 4
    public static final int STYLE_STRIKETHROUGH = 1 << 3; // 8

    ...
    void execute(){
        //use the bitwise OR operation to combine several constants into a set
        text.applyStyles(STYLE_BOLD | STYLE_ITALIC);

    }
}
```

The bit field representation also lets you preform set operations such as union and intersection using bitwise arithmetic.

### Disadvantages

It is hard to interpret a bit field than a simple `int` enum constant when it is printed as a number.

There is no easy way to iterate over all of the elements represented by a bit field.

You have to predict the maximum number of bits you'll need at the time you're writing the API and choose a type for the bit field (typically `int` or `long`) accordingly. Once you've picked a type, you can't exceed its width without changing the API.

## The `EnumSet`

- Implements the `Set` Interface,, but internally, each `EnumSet` is represented as a bit vector.

### Why

This allows for the bitwise arithmetic used in bit fields, as well as all of the benefits of [using enums](./item-34-use-enums-instead-of-constants.md).

### Why not a `HashSet`?

This could also be used, but `HashSet` is designed as a general-purpose `Set` implementation. To achieve optimal performance for enums collected in `Set`s, use an `EnumSet`.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-35-use-instance-fields-instead-of-ordinals.md)
- [Next](./item-37-use-enummap-instead-of-ordinal-indexing.md)
