# Item 23: Prefer class hierarchies to tagged classes

## Main Takeaway

> Tagged classes are seldom appropriate. If you're tempted to write a class with an explicit tag field, think about whether the tag could be eliminated and the class replaced by a hierarchy. When you encounter an existing class with a tag field, consider refactoring it into a hierarchy.

## Rationale

Tagged classes are verbose, error-prone, and inefficient, can are simply "a [pallid](https://www.merriam-webster.com/dictionary/pallid) imitation of a class hierarchy."

## What exactly is a "tagged class?"

```java
/** Tagged class - vastly inferior to a class hierarchy! (Page 109)
 * 
 * https://github.com/jbloch/effective-java-3e-source-code/blob/master/src/effectivejava/chapter4/item23/taggedclass/Figure.java
 */
class Figure {
    enum Shape { RECTANGLE, CIRCLE };

    // Tag field - the shape of this figure
    final Shape shape;

    // These fields are used only if shape is RECTANGLE
    double length;
    double width;

    // This field is used only if shape is CIRCLE
    double radius;

    // Constructor for circle
    Figure(double radius) {
        shape = Shape.CIRCLE;
        this.radius = radius;
    }

    // Constructor for rectangle
    Figure(double length, double width) {
        shape = Shape.RECTANGLE;
        this.length = length;
        this.width = width;
    }

    double area() {
        switch(shape) {
            case RECTANGLE:
                return length * width;
            case CIRCLE:
                return Math.PI * (radius * radius);
            default:
                throw new AssertionError(shape);
        }
    }
}
```

## Converting "tagged classes" into a class hierarchy

1. Define an abstract class containing an abstract method for each method in the tagged class whose behavior depends on the tag value. This abstract class is the root of the class hierarchy.
2. If there are any methods whose behavior does not depend on the value of the tag, put them in this abstract class.
3. Define a concrete subclass of the root class for each flavor of the original tagged class, and include the following:
      1. The data fields particular to its flavor.
      2. The appropriate implementation of each abstract method in the root class.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-22-use-interfaces-only-to-define-types.md)
- [Next](./item-23-prefer-class-hierarchies-to-tagged-classes.md)
