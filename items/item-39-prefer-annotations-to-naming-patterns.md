# Item 39: Prefer annotations to naming patterns

> If you write a tool that requires programmers to add information to source code, define appropriate annotation types. **There is simply no reason to use naming patterns when you can use annotation instead.**
>
> That said, with the exception of toolsmiths, most programmers will have no need to define annotation types. **But all programmers should use the predefine annotation types that Java provides (such as `@Override` or `@SuppressWarnings`)**.

## The disadvantages of naming patterns

1. Typographical errors result in silent failures.
2. There is no way to ensure that they are used only on appropriate program elements.
3. They provide no good way to associate parameter values with program elements.

## Annotations - Primer

### Meta-Annotations

Annotations that annotate other annotations.

- `@Retention` - indicates how long annotations should be retained within the applications lifecycle (e.g. `@Retention(RetentionPolicy.RUNTIME)` to keep annotations at runtime).

### Marker Annotations

A parameterless annotation used to simply "mark" annotated content.

### Annotation Processing API

Source-level annotation processing that first appeared in Java 5, that can generate additional source files during the compilation stage.

The source files don’t have to be Java files — you can generate any kind of description, metadata, documentation, resources, or any other type of files, based on annotations in your source code.

NOTE: the annotation processing API  can only be used to generate new files, not to change existing ones.

### Parameter Arrays

The syntax for array parameters in annotations is flexible. It is optimized for single-element arrays. To specify a multiple-element array, surround the elements with curly braces and separate them with commas.

### Repeated annotations

As of Java 8, you can annotate the declaration of an annotation with the @Repeatable meta-annotation to indicate that the annotation may be applied repeatedly to a single element. This meta-annotation takes a single parameter, which is the class object of a containing annotation type, whose sole parameter is an array of the annotation type.

To detect repeated and non-repeated annotations with `isAnnotationPresent`, you must check for both the annotation type and its containing annotation type.

Repeatable annotations were added to improve the readability of source code that logically applies multiple instances of the same annotation type to a given program element. If you feel they enhance the readability of your source code, use them, but remember that there is more boilerplate in declaring and processing repeatable annotations, and that processing repeatable annotations is error-prone.

(WIP: add example code here)

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-38-emulate-extensible-enums-with-interfaces.md)
- [Next](./item-40-consistently-use-the-override-annotation.md)
