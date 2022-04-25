# Item 2: Consider a builder when faced with many constructor parameters

## Main Takeaway

> Instead of making the desired object directly, the client calls a constructor (or static factory) with all of the required parameters and gets a _builder object_. Then the client calls setter-like method on the builder object to set each optional parameter of interest. Finally, the client calls a parameterless build method to generate the object, which is typically immutable.

## What is a Builder?

The Builder Pattern (in the context) is the process of calling a separate a "builder" object (or static factory method) with all of the required / optional parameters to generate an individual object, instead of making the desired object direclty. This allows for flexibility in object constrcution, while also allowing for the desired output object to be immutable.

```java
PersonBuilder builder = new PersonBuilder();
Person bob = builder.firstName("Bob")
                    .lastName("Builder")
                    .age(33)
                    .description("Man I love building stuff!")
                    .build();
```

The process is similar to using StringBuilder.

## Why this is useful

> A minor advantage of builders over constructors is that builders can have multiple varargs parameters because each parameter is specified in its own method.  
> …
> [T]he Builder pattern is a good choice when designing classes who constructors or static factories would have more than a handful of [optional] parameters.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-01.md)
- [Next](item-03.md)
