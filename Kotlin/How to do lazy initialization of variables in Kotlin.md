# How to do Lazy Initialization of Variables in Kotlin

Kotlin provides two main ways to initialize variables lazily:

## 1. Using `lazy` for Immutable Properties
The `lazy` delegate is used for read-only (`val`) properties and ensures that the variable is initialized only when accessed for the first time.

### Example:
```kotlin
val lazyValue: String by lazy {
    println("Initializing...")
    "Hello, Kotlin!"
}

fun main() {
    println("Before accessing lazyValue")
    println(lazyValue) // Initialization happens here
    println(lazyValue) // This time, the cached value is returned
}
```
**Output:**
```
Before accessing lazyValue
Initializing...
Hello, Kotlin!
Hello, Kotlin!
```

## 2. Using `lateinit` for Mutable Properties
The `lateinit` modifier is used for `var` properties when initialization needs to be delayed but the value will be assigned before usage.

### Example:
```kotlin
class Example {
    lateinit var message: String

    fun initialize() {
        message = "Hello, Kotlin!"
    }

    fun printMessage() {
        if (::message.isInitialized) {
            println(message)
        } else {
            println("Message is not initialized yet")
        }
    }
}

fun main() {
    val example = Example()
    example.printMessage() // Not initialized yet
    example.initialize()
    example.printMessage() // Now prints the message
}
```
**Key Differences:**
- `lazy` is used for `val` and ensures thread-safe initialization.
- `lateinit` is used for `var` and requires manual initialization before access.

Using these techniques, you can optimize resource usage and initialization logic in your Kotlin applications.
