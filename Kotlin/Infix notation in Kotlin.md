# Infix Notation in Kotlin

Kotlin provides a special way to call functions with a single parameter using infix notation. This makes the code more readable and resembles natural language.

## Syntax
To define an infix function, the following conditions must be met:
1. It must be a member function or an extension function.
2. It must have a single parameter.
3. It must be marked with the `infix` keyword.

## Example

```kotlin
class Person(val name: String) {
    infix fun greet(message: String) {
        println("$name says: $message")
    }
}

fun main() {
    val person = Person("Alice")
    person greet "Hello, Kotlin!" // Infix notation
    person.greet("Hello, Kotlin!") // Normal function call
}
```

## Advantages of Infix Notation
- Improves code readability.
- Makes function calls more expressive.
- Works well for operations that logically resemble infix expressions, such as mathematical operations or custom DSLs.

## Common Use Cases
- Defining custom operators (e.g., `to` in `mapOf("key" to "value")`).
- Creating expressive domain-specific languages (DSLs).
- Simplifying function calls in chaining operations.

### Example: Using `to` as an Infix Function

```kotlin
val pair = "language" to "Kotlin"
println(pair) // Output: (language, Kotlin)
```

Infix notation can make function calls more intuitive and is widely used in Kotlin's standard library.
