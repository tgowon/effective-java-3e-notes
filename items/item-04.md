# Item 4: Enforce noninstantiability with a private constructor

When creating a utility class (e.g. when grouping static methods, including factory methods, for objects that implement a particular interface, in the manner of `java.util.Collections`), explicitly provide a private constructor to ensure noninstantiability.

```java
**// Noninstantiable utility class**
public class UtilityClass {
    **// Suppress default constructor for noninstantiability**
    private UtilityClass() {
        throw new AssertionError();
    }
    ...  // Remainder omitted
}
```

**Why?**

- In the absence of explicit constructors the compiler provides a public, parameterless _default constructor_, undistinguishable from any other constructor.

**Can you enforce noninstantiability by making a class abstract?**

- No. The class can be subclassed and the subclass instantiated. It also misleads the user into thinking the class was designed for inheritance.

**Do you need the `AssertionError`?**

- No. The AssertionError isn’t strictly required, but it provides insurance in case the constructor is invoked, either: accidentally from within the class, or from some other means (reflection?)

**Any Gotchas?**

- Note: this prevents the class from being subclassed.
- All constructors must invoke a superclass constructor, explicitly or implicitly; therefore a subclass would have no accessible superclass constructor to invoke.
