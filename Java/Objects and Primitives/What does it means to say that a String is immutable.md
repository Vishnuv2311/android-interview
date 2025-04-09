In Java, saying that a `String` is immutable means that once a `String` object is created, its value cannot be changed. Any operation that appears to modify a `String` (e.g., concatenation, substring, or replacement) actually creates a new `String` object rather than altering the original one.

### Key Points:
- **Thread Safety**: Immutability makes `String` inherently thread-safe, as multiple threads can safely share the same `String` instance without synchronization.
- **String Pool**: Java uses a special memory area called the "String Pool" to store `String` literals. Immutability allows reusing `String` objects, reducing memory overhead.
- **Security**: Since `String` objects cannot be modified, they are often used in security-sensitive contexts like passwords, class loading, and network connections.

Example:
```java
String str = "Hello";
str = str + " World"; // A new String object is created, "Hello World"
```
In the example above, the original `String` "Hello" remains unchanged, and a new `String` object is created for "Hello World".
