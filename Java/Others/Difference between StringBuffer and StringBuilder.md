### Difference between StringBuffer and StringBuilder

1. **Thread Safety**:
   - `StringBuffer` is thread-safe as its methods are synchronized.
   - `StringBuilder` is not thread-safe and is designed for single-threaded environments.

2. **Performance**:
   - `StringBuffer` is slower due to synchronization overhead.
   - `StringBuilder` is faster as it does not have synchronization.

3. **Usage**:
   - Use `StringBuffer` when working in a multi-threaded environment.
   - Use `StringBuilder` for better performance in single-threaded scenarios.

### Examples

#### StringBuffer Example
```java
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}
```

#### StringBuilder Example
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}
```
