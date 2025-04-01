# String vs StringBuffer vs StringBuilder in Kotlin

In Kotlin (and Java), there are three main ways to work with strings: `String`, `StringBuffer`, and `StringBuilder`. Each has different characteristics and use cases.

## 1. String
- **Immutable**: Once created, a `String` object cannot be modified.
- **Thread-Safe**: Since `String` is immutable, it is inherently thread-safe.
- **Performance**: Slower when performing multiple modifications because each operation creates a new `String` object.

**Example:**
```kotlin
val str1 = "Hello"
val str2 = str1 + " World" // Creates a new String object
println(str2) // Output: Hello World
```

## 2. StringBuffer
- **Mutable**: Allows modifications without creating new objects.
- **Thread-Safe**: It is synchronized, meaning multiple threads can use it safely.
- **Performance**: Slower than `StringBuilder` due to synchronization overhead.

**Example:**
```kotlin
val sb = StringBuffer("Hello")
sb.append(" World")
println(sb.toString()) // Output: Hello World
```

## 3. StringBuilder
- **Mutable**: Like `StringBuffer`, it allows modifications.
- **Not Thread-Safe**: It is not synchronized, making it faster than `StringBuffer` in a single-threaded environment.
- **Performance**: Faster than `StringBuffer` when used in a single-threaded application.

**Example:**
```kotlin
val sb = StringBuilder("Hello")
sb.append(" World")
println(sb.toString()) // Output: Hello World
```

## Key Differences:
| Feature       | String           | StringBuffer      | StringBuilder     |
|--------------|----------------|----------------|----------------|
| Mutability   | Immutable       | Mutable        | Mutable        |
| Thread Safety | Yes             | Yes (Synchronized) | No (Not Synchronized) |
| Performance  | Slow for modifications | Slower due to synchronization | Fastest |

## When to Use What?
- Use `String` when working with fixed or small amounts of text.
- Use `StringBuffer` when multiple threads need to modify the same string.
- Use `StringBuilder` for better performance in a single-threaded environment.
