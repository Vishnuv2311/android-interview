### How is the String class implemented?

The `String` class in Java is implemented as a final class, meaning it cannot be subclassed. Internally, it uses a character array (`char[]`) to store the sequence of characters. In Java 9 and later, the internal representation was optimized to use a byte array (`byte[]`) along with an encoding flag to save memory for ASCII strings.

Key characteristics of the `String` class:
- It is immutable, meaning once a `String` object is created, its value cannot be changed.
- It overrides methods from the `Object` class, such as `equals()` and `hashCode()`, to provide value-based equality and hashing.
- It is optimized for performance, with features like string pooling.

### Why was the String class made immutable?

1. **Thread Safety**: Immutability ensures that `String` objects can be safely shared between multiple threads without synchronization.

2. **String Pooling**: The Java String Pool allows for the reuse of `String` objects, reducing memory usage. Immutability ensures that strings in the pool are not modified.

3. **Security**: Strings are often used in sensitive operations like file paths, network connections, and class loading. Immutability prevents malicious or accidental modification.

4. **Hashing**: Strings are commonly used as keys in hash-based collections like `HashMap`. Immutability ensures that the hash code of a `String` remains constant, preventing issues with key lookups.

5. **Performance**: Since `String` objects are immutable, they can be cached and reused without the need for defensive copying.

By making the `String` class immutable, Java ensures reliability, security, and efficiency in its core operations.
