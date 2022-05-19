
# Item 35: Use instance fields instead of ordinals

## Main Takeaway

> All enums have an `ordinal` method, which returns the numerical position of each enum constant in its type.  Unless you're writing code [the creates/uses general-purpose enum-based data structures such as `EnumSet` and `EnumMap`], you are best off avoiding the `ordinal` method entirely.

## Alternative - Instance Fields Example

```java
// Abuse of ordinal to derive an associated value - DON'T DO THIS
public enum Ensemble{
    SOLO, DUET, TRIO;
}

// Add an instance field to ensure the meaning of the ordered enum
// doesn't rely on the built in `ordinal` method.
public enum Ensemble{
    SOLO(1), DUET(2), TRIO(3);

    private final int musicians;
    Ensemble(int size){
        this.musicians = size;
    }
    public int musicians(){
        return this.musicians;
    }
}
```

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-34-use-enums-instead-of-constants.md)
- [Next](./item-35-use-instance-fields-instead-of-ordinals.md)
