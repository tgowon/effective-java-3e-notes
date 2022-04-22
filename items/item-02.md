# Item 2: Consider a builder when faced with many constructor parameters

The gist:  

> Instead of making the desired object directly, the client calls a constructor (or static factory) with all of the required parameters and gets a _builder object_. Then the client calls setter-like method on the builder object to set each optional parameter of interest. Finally, the client calls a parameterless build method to generate the object, which is typically immutable.

Why this is useful:  

> A minor advantage of builders over constructors is that builders can have multiple varargs parameters because each parameter is specified in its own method.  
> …
> [T]he Builder pattern is a good choice when designing classes who constructors or static factories would have more than a handful of [optional] parameters.
