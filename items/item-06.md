# Item 6: Avoid creating unnecessary objects

## Main Takeaway

>It is often appropriate to reuse a single object instead of creating a new functionally equivalent object each time it is needed. Reuse can be both faster and more stylish. An object can always be reused if it is immutable.
>
>You can often avoid creating unnecessary objects by using **static factory methods** (Item 1) in preference to constructors on immutable classes that provide both.

## On Autoboxing

>Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
Autoboxing (i.e. primitive-to-object two-way transformation) is another way to create unnecessary objects. Autoboxing blurs but does not erase the distinction between primitive and boxed primitive types.

```java
//Hideously slow! 2^31 unnecessary Long instances created.
private static long sum {
    Long sum = 0L;
    for (long i = 0; i<= Integer.MAX_VALUE; i++){
        sum +=i;
    }
    return sum;
}
```

## Counter-Argument Takeaways

- The creation and reclamation of small objects whose constructors do little explicit work is cheap, especially on modern JVM implementations. Creating additional objects to enhance the clarity, simplicity, or power of a program is generally a good thing.
- Avoiding object creation by maintaining your own object pool is a bad idea unless the objects in the pool are extremely heavyweight. Modern JVM implementations have highly optimized GC that easily outperform such object pools on lightweight objects.
- Also, see Item 50 on defensive copying. Note that "the penalty for reusing an object when defensive copying is called for is far greater than the penalty for needlessly creating a duplicate object. Failing to make defensive copies where required can lead to insidious bugs and security holes; creating objects unnecessarily merely affects style and performance."

### Lazy-initializing classes

**Pro-Tip on Pattern Matching:** When Pattern Matching in Java (i.e. using a `Pattern` instance); prefer to initialize the instance as a part of class initialization (i.e. as a `static final` instance on the class), cache it, and reuse the same instance for every invocation on a given method. This is because pattern matching is not suitable for repeated use in performance-critical situations.

When you create a `Pattern` / regular expression locally that is used in a method, internally the system creates a  `Pattern`  instance, uses it once, and then marks it eligible for garbage collection. Creating `Pattern` instances is expensive because it requires compiling the regular expression into a finite state machine. If instead you initialized the `Pattern` at the class level (via a `static final` field), you instead create this finite state machine only one time, and use it across multiple method invocations.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-05.md)
- [Next](item-07.md)
