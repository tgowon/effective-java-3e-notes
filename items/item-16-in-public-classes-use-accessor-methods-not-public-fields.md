# Item 16: In public classes, use accessor methods, not public fields

## Main Takeaway

> Public classes should never expose mutable fields. It is less harmful, though still questionable, for public classes to expose immutable fields. It is, however, sometimes desireable for package-private or private nested classes to expose fields, whether mutable or immutable.

If a class is accessible outside its package, provide accessor methods to preserve the flexibility to change the class's internal representation.

```java
//Bad design -- does not offer Data Encapsulation Benefits
public class Point{
    public double x;
    public double y;
}
```

If a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields -- assuming they do an adequate job of describing the abstraction provided by the class. This approach generates less visual clutter than the accessor-method approach, both in the class definition and in the client code that uses it.

```java
//Graph is public
public class Graph{
    //OK - class inaccessible outside of top-level "Graph"
    private class Point{
        double x;
        double y;
    }

    //Remainder Omitted
}
```

While it's never a good idea for a public class to expose fields directly, it is less harmful if the fields are immutable. You can't change the representation of such a class without changing its API, and you can't take auxiliary actions when a field is read, but you can enforce invariants.

```java
// Public class with exposed immutable fields - questionable   (Page 79)
public final class Time {
    private static final int HOURS_PER_DAY    = 24;
    private static final int MINUTES_PER_HOUR = 60;

    public final int hour;
    public final int minute;

    public Time(int hour, int minute) {
        if (hour < 0 || hour >= HOURS_PER_DAY)
            throw new IllegalArgumentException("Hour: " + hour);
        if (minute < 0 || minute >= MINUTES_PER_HOUR)
            throw new IllegalArgumentException("Min: " + minute);
        this.hour = hour;
        this.minute = minute;
    }

    // Remainder omitted
}
```

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-15-minimize-the-accessibility-of-classes-and-members.md)
- [Next](./item-17-minimize-mutability.md)
