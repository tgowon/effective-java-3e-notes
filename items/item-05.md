# Item 5: Prefer dependency injection to hardwiring resources

> Do not use a singleton or static utility class to implement a class that depends on one or more underlying resources whose behavior affects that of the class, and do not have the class create these resources directly. Instead, pass the resources, or factories to create them, into the constructor (or static factory or builder). This practice, known as **dependency injection**, will greatly enhance the flexibility, reusability, and testability of the class.

According to Effective Java, here are some bad times --

**Inappropriate use of static utility:**  

```java
//Inappropriate use of static utility - inflexible & untestable
public class SpellChecker {
    private static final Lexicon dictionary = Lexicon.INSTANCE; //This is inflexible!
    private SpellChecker(){}// Noninstantiable

    public static boolean isValid(String word) {/*...*/}

    public static List<String> suggestions(String typo){/*...*/}
}
```

**Inappropriate use of singleton:**  

```java
//Inappropriate use of singleton - inflexible & untestable
public class SpellChecker {
    private static final Lexicon dictionary = Lexicon.INSTANCE; //This is STILL inflexible!
    private SpellChecker(){}// Noninstantiable

    public static SpellChecker INSTANCE = new SpellChecker();

    public static boolean isValid(String word) {/*...*/}

    public static List<String> suggestions(String typo){/*...*/}
}
```

> :information_source: Side note:  While I think I'm used to hearing “Dependency Injection” and thinking about Spring (or Guice, etc.), in reality, dependency injection can simply be a constructor param pass-through:

**Dependency Injection provides flexibility and testability:**  

```java
//Dependency Injection provides flexibility and testability 
public class SpellChecker {
    private final Lexicon dictionary; // now initialized in constructor

    public SpellChecker(Lexicon dict){
        this.dictionary = Objects.requireNonNull(dict);
    }
    public static boolean isValid(String word) {/*...*/}
    public static List<String> suggestions(String typo){/*...*/}
}

```

In addition, you can also pass in a factory to the constructor; or, since JDK8, a `Supplier<T>` interface.

Just know that once you start implementing your own manual dependency injection, things can start to get cluttered. The suggestion is to use a true Dependency Injection Framework; but I think we’re well aware of the pros and cons of that as well.

## Navigation

- [All Items](../README.md#items)
- [Previous](item-04.md)
- [Next](item-06.md)