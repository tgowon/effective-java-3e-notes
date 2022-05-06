# Item 22: Use interfaces only to define types

## Main Takeaway

> Interfaces should be used only to define types. They should not be used merely to export constants.

## Alternatives

1. Add your constants directly to your class.
2. Export your constants with an [`enum` type](./item-34-use-enums-instead-of-constants.md).
3. Export the constants with a [non-instantiable utility class](./item-04-enforce-non-instantiability-with-a-private-constructor.md).

## Pro-tips

### Consider adding underscores to numeric literals

```java
//Example: underscores and exponent "e" allowed in numeric literals.
package dev.tgowon;
public class Constants{
    private Constants(){} // Prevents Instantiation

    public static final double AVOGADROS_NUMBER = 6.022_140_857e23;
    public static final double ELECTRON_MASS = 9.109_383_56e-31;
}
```

### Consider `static import` for groups of constants

```java
import static dev.tgowon.Constants.*;

public class Test{
    double atoms(double mols){
        return AVOGADROS_NUMBER * mols;
    }
    ...
    //etc
}
```

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-21-design-interfaces-for-posterity.md)
- [Next](./item-22-use-interfaces-only-to-define-types.md)
