# Item 11: Always override hashCode when you override equals

## Main Takeaway

> You _must_ override `hashCode` every time you override `equals` or your program will not run correctly. Your `hashCode` method must obey the general contract specified in `Object` and must do a reasonable job assigning unequal has codes to unequal instances.

## Rationale

Values return from `hashCode` must satisfy the following criteria:

1. **When the `hashCode` method is invoked on an object repeatedly during an execution of an application, it must consistently return the same value, provide no information used in the `equals` comparisons is modified.** This value ned to remain consistent from one execution of an application to another.
2. **If two objects are equal according to the `equals(Object)` method, then calling `hashCode` on the two objects must product the same integer result.**
3. **If two objects are unequal according to the `equals(Object)` method, it is _not_ required that calling the hashCode on each of the objects must product distinct results.** However, the programmer should be aware that producing distinct results for unequal objects my improve the performance of hash tables.

Since equal objects must have equal hash codes, overriding `equals` requires overriding `hashCode` for the methods to remain consistent and in compliance.

Example: if your goal is to provide update the equivalence relation (`equals`) so that the following Java code functions properly, overriding `hashCode` is essential:

```java
Map<PhoneNumber, String> m = new HashMap<>();
m.put(new PhoneNumber(707,867,5309), "Jenny");

String result =  m.get(new PhoneNumber(707,867,5309)); 

// If hashCode has been overridden correctly: "Jenny"
// If not: null 
System.out.println(result);
```

## Pro-Tips: Designing a good  `hashCode` method

### Don't provide a detailed `hashCode` specification in your documentation

> Don't provide a detailed specification for the value returned by `hashCode`, so clients can't reasonable depend on it; this gives you flexibility to change it.

If you leave the details unspecified and a flaw is found in the function or a better has function is discovered, you have change it in a subsequent release.

### Provide unequal hash codes for unequal instances

```java
// While legal, don't do this!
@Override 
public int hashCode(){
    return 123;
}
```

The example above is legal because it ensures equal objects have the same hashCode. But it also ensures _every_ object has the same hash code.

### When in doubt, let a machine do it for you

Modern IDEs, as well as Google's AutValue framework can generate a decent `hashCode` method.

There are also libraries that provide production-ready hash functions, such as Google Guava's `com.google.common.hash.Hashing`.

The `Objects` class in Java also has a static method for producing hash functions, but this method has performance concerns.

```java
// In Objects.java
public static int hash(Object... values){...}
```

**Note:** behind the scenes, `Objects.hash()` is actually calling the following method in `Arrays.java`:

```java
public static int hashCode(Object a[]) {
    if (a == null)
        return 0;

    int result = 1;

    for (Object element : a)
        result = 31 * result + (element == null ? 0 : element.hashCode());

    return result;
}
```

#### Why `31`?

> The value 31 was chosen because it is an odd prime. If it were even and teh multiplication overflowed, information would be lost, because multiplication by 2 is equivalent to shifting. The advantage of using a prime is less clear, but it is traditional. A nice property of 31 is that the multiplication can be replaced by a shift and a subtraction for better performance on some architectures: `31*i == (i<<5) - i`. Modern VMs do this sort of optimization automatically.

### If you need to create your own `hashCode` implementation, follow a recipe

Pp. 51-51 in _Effective Java_ provide a recipe that is very similar to the implementation found in `Arrays.java`. You can also find efficient open-source algorithms on the Internet.

#### If you're implementing your own hashCode, considering the following tips

- Exclude any fields that are not used in `equals` comparisons, or your risk violating the second provision of the hashCode contract
- Do not be tempted to exclude significant fields from the hashCode computation to improve performance.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-10.md)
- [Next](item-12.md)
