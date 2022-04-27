# Item 9: Prefer `try-with-resources` to `try-finally`

## Main Takeaway

> Always use `try-with-resources` in preference to `try-finally` when working with resources that must be closed. The resulting code is shorter and clearer, and the exceptions that it generates are more useful.

### `try-finally` - potentially ugly code

```java
//try-finally is ugly when used with more than one resource!
static void copy(String src, String dst) throws IOException{
    InputStream in = new FileINputStream(src);
    try{
        OutputStream out = new FileOutputStream(dst);
        try{
            byte[] buf = new byte[BUFFER_SIZE];
            int n;
            while((n=in.read(buf)) >= 0){
                out.write(buf,0,n);
            }
        }finally{
            out.close();
        }
    } finally{
        in.close();
    }
}
```

### Same block written w/ `try-with-resources`

```java
//try-with-resources on multiple resources - short and sweet
static void copy(String src, String dst) throws IOException{
    try(
        //multiple statements within "try" parens
        InputStream   in = new FileInputStream(src);
        OutputStream out = new FileOutputStream(dst)
    ){
        byte[] buf = new byte[BUFFER_SIZE];
        int n;
        while((n=in.read(buf)) >= 0){
            out.write(buf,0,n);
        }
    }
}
```

### Similarities

- Neither are inherently "wrong," `try-with-resources` provides several style/clarity advantages.
- Both can also use a `catch` block to manage exceptions.
  
```java
    try{
        FooResource foo = FooResource.newInstance();
        foo.execute();
    } catch(Exception e){
        log.error("Bad thing happened", e);
    } finally{
        foo.close();
    }

    //vs.
    try(FooResource foo = FooResource.newInstance()){
        foo.execute();
    } catch(Exception e){
        log.error("Bad thing happened", e);
    }
```

### Differences

- `try-finally`
  - Need to explicitly close each resource within a (separate) finally
    - Can get nested / ugly / hard to read.
  - If exception occurs in both `try` _and_ `finally` only the second (`finally`)     exception is surfaced in the stacktrace:
    - > there is no record of the first exception in the exception stack trace, which can greatly complicate debugging in real systems.
      - It's possible to write code to suppress the second (`finally`) exception, but this can make your code even harder to read.
- `try-with-resources`
  - concise (compared to `try-finally`)
  - If exceptions are thrown in the `try` clause and the (invisible) `close()`, the latter is _suppressed_ in order to keep the first exception visible.
    - _Suppressed_ exceptions are printed to the stack tract with a notation saying that they were suppressed. You can get them programmatically by calling `getSuppressed()` on the `Throwable` (since JDK 7).

## Navigation

- [All Items](../README.md#items)
- [Previous](./item-08-avoid-finalizers-and-cleaners.md)
- [Next](./item-10-obey-the-general-contract-when-overriding-equals.md)
