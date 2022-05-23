# Item 37: Use `EnumMap` instead of ordinal indexing

## Main Takeaway

> It is rarely appropriate to use ordinals to index into arrays: use `EnumMap` instead. If the relationship you are representing is multidimensional, use `EnumMap<...,EnumMap<...>>`. This is a special case of the general principle that [application programmers should rarely, if ever, use `Enum.ordinal`](./item-35-use-instance-fields-instead-of-ordinals.md).

## The `EnumMap`

- Implements the `Map` Interface, but internally, each `EnumMap` is represented as a bit as an array.

Per the JavaDocs:

>Enum maps are represented internally as arrays. This representation is extremely compact and efficient.
>
>Implementation note: All basic operations execute in constant time. They are likely (though not guaranteed) to be faster than their HashMap counterparts.

### Why not a `HashMap`?

This could also be used, but `HashMap` is designed as a general-purpose `Map` implementation. To achieve optimal performance for enums collected in `Maps`s, use an `EnumMap`.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-36-use-enumset-instead-of-bit-fields.md)
- [Next](./item-38-emulate-extensible-enums-with-interfaces.md)
