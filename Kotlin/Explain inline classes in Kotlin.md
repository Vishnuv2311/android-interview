## Inline Classes in Kotlin

### Introduction
Inline classes in Kotlin provide a way to wrap a value inside a type without adding runtime overhead. They are useful when you want to create a type-safe abstraction over a primitive type or any other type.

### Syntax
An inline class is defined using the `inline` keyword before the `class` keyword:

```kotlin
@JvmInline
value class UserId(val id: String)
```

### Key Features
- **No runtime overhead**: The compiler optimizes inline classes by removing the wrapper at runtime.
- **Type safety**: Ensures that specific types are used where expected.
- **Can have properties but no backing fields**: Inline classes can only have read-only properties.

### Example Usage
```kotlin
@JvmInline
value class Email(val value: String)

fun sendEmail(email: Email) {
    println("Sending email to: ${email.value}")
}

fun main() {
    val email = Email("test@example.com")
    sendEmail(email)
}
```

### Limitations
- Cannot have `init` blocks.
- Cannot store multiple properties.
- Cannot inherit from other classes or be inherited.

### Conclusion
Inline classes improve type safety while maintaining efficiency by avoiding unnecessary object creation. They are particularly useful in scenarios where primitive-like efficiency is required with additional type safety.
