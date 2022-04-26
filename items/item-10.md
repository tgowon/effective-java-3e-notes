# Item 10: Obey the General Contract when Overriding Equals

## Main Takeaway

> Don't override the `equals` method unless you have to: in many cases, the implementation inherited from `Object` does exactly what you want. If you override `equals`, make sure to compare all of the class's significant fields and to compare them in a manner that preserves all five provisions of the `equals` contract.

## Notes

A programmer who compares references to value objects using the `equals` method expects to find out whether they are logically equivalent, not whether they refer to the same object.

One kind of value class that does _not_ require the `equals` method to be overridden is a class that uses instance control (Item 1) to ensure that at most one object exists with each value. (like Enums)

The `equals` method implements an _equivalence relation._

## What is an Equivalence Relation?

### Reflexive

> For any non-null reference value `x`, `x.equals(x)` must return `true`.

If you were to violate this property and then add an instance of your class to a collection, the `contains` method might well say that the collections didn't contain the instance that you just added.

### Symmetric

> For any non-null reference values `x` and `y`, `x.equals(y)` must return `true` if and only if `y.equals(x)` returns `true`.

Once you've violated the `equals` contract (with respect to symmetry), you simply don't know how other objects will behave when confronted with your object.

### Transitive

> For non-null reference values `x`, `y`,`z`, if `x.equals(y)` returns `true` and `y.equals(z)` returns `true`, then `x.equals(z)` must return true.

There is no way to extend an instantiable class and add a value component while presenving the `equals` contract.

You can add a value component to a sublcass of an _abstract_ class without violating the `equals` contract. Problems of the sort shown earlier won't occur so long as it is impossible to create a superclass instance directly.

### Consistent

>For any non-null reference values, `x` and `y`, multiple invocations of `x.equals(y)` must consistently return `true` or consistently return `false`, provided no information used in `equals` comparisons is modified. 

Do not write an `equals` method that depends on unreliable resources. ... To avoid this sort of problem, `equals` should only perform on deterministic computations on memory-resident objects.

### Non-`null`-ability

> For any non-null reference value `x`, `x.equals(null)` must return `false`.

Your `equals` method should return `false` on null not `NullPointerException`.

Note: the `instanceof` operator does an implicit `null` check, so you don't have to do an explicit `null` check in your `equals` method.

## Pro-Tips: Designing a good `equals` method

### Always override hashCode when you override equals

See [Item 11](item-11.md).

### Don't substitute another type for `Object` in the `equals` declaration

If you change the contract, you are no longer overriding Object.equals, and instead _overloading_ `equals`. This will result in two separate equals methods on your class.

```java
//Broken - parameter type must be Object!
public boolean equals(MyClass o){...}
```

Note: simply adding `@Override` will not override an overloaded method.

```java
//Also Broken, now won't compile
@Override
public boolean equals(MyClass o){...}
```

### Don't try to be too clever

Keep it simple, and adhere to the [Equivalence Relations](#what-is-an-equivalence-relation). Test your code thoroughly

### If you need help, follow a good guide

Pp. 47-48 in _Effective Java_ provide a recipe for building an efficient `equals` method. The following is a brief overview.

1. Use the `==` operator to check if the argument is a referrence to `this` object.
2. Use the `instanceof` operator to check if the argument has the correct type.
3. Cast the argument to the correct type
4. For each "significant" field in the class, check if that field of the argument matches the corresponding field of `this` object.


You can also find efficient open-source algorithms on the Internet.

### When in doubt, let a machine do it for you

Modern IDEs, as well as Google's AutValue framework can generate a decent `equals()` method.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-09.md)
- [Next](item-11.md)
