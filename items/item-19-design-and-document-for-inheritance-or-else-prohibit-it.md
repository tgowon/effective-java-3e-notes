# Item 19: Design and document for inheritance or else prohibit it

## Main Takeaway

> [When designing a class for inheritance] you must document all of its self-use patterns, and once you've documented them, you must commit to them for the life of the class. If you fail to do this, subclasses may become dependent on implementation details of the superclass and may break if the implementation of the superclass changes. To allow other to write _efficient_ subclasses, you may have to export one or more protected methods. Unless you know there is a real need for subclasses, you are probably better off prohibiting inheritance by declaring your class `final` or ensuring that there are no accessible constructors.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-18-favor-composition-over-inheritance.md)
- [Next](./item-19-design-and-document-for-inheritance-or-else-prohibit-it.md)
