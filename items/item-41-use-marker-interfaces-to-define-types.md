# Item 41: Use marker interfaces to define types

## Main Takeaway

> marker interfaces and marker annotations both have their uses. If you want to define a type that does nto have any new methods associated with it, a marker interface is the way to go. If you want to mark program elements other than classes and interfaces or to fit the marker into a framework that already makes heavy use of annotation types, then a market annotation is the correct choice. If you find yourself writing a market annotation type whose target is `ElementType.TYPE`, take the time to figure out whether it really should be an annotation type or whether a marker interface would be more appropriate.

## What is a "marker interface"?

A _marker interface_ is an interface that contains no method declarations but merely designates (or "marks") a class that implements the interface as having some property.

## Marker Interfaces vs. Marker Annotations

### Marker Interfaces - Benefits

1. Marker interfaces define a type that is implemented by instances of the marked class; marker annotations do not.
   1. This (the interface) allows you to catch errors at compile time that an annotation would not.
2. Marker interfaces can be targeted more precisely than marker annotations
   1. Marker interfaces can extend any interface; therefore you can use it to extend the sole interface which the market is applicable, guaranteeing that all marked types are also subtypes of that interface.
      1. **Why is this useful?** Such a marker interface might describe some invariant of the entire object or indicate that instances are eligible for processing by a method of some other class.
   2. `ElementType.TYPE` cannot be this precise, since it can be applied to any class / interface.

### Marker Annotations - Benefits

1. Marker annotations can leverage the larger annotation framework.
   1. If your marker use-case goes beyond classes/types to methods, fields, etc., then using a marker annotations makes the most sense.
      1. In fact, it is the _only_ marker solution you can use in this case, as marker interfaces can _only_ be used for classes/types.

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-40-consistently-use-the-override-annotation.md)
- [Next](./item-41-use-marker-interfaces-to-define-types.md)
