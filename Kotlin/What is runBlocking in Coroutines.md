# What is runBlocking in Coroutines?

`runBlocking` is a function in Kotlin Coroutines that bridges the gap between regular blocking code and coroutine-based code. It is primarily used in main functions and tests to start coroutines in a blocking manner.

## Key Features:
- It **blocks the current thread** until the coroutine inside completes execution.
- Used mainly in **unit tests and main functions**.
- Not recommended for use inside coroutines or UI applications as it can lead to thread blocking.

## Example:

```kotlin
import kotlinx.coroutines.*

fun main() {
    println("Before runBlocking")

    runBlocking {
        launch {
            delay(1000L)
            println("Inside runBlocking coroutine")
        }
    }

    println("After runBlocking")
}
```

### When to Use `runBlocking`:
- To start coroutines in **non-coroutine environments** (like the `main` function).
- In **unit tests** where you need to execute coroutines sequentially.
- When you need to **bridge blocking and suspending** code.

### When NOT to Use:
- Inside an already running coroutine.
- In UI applications, as it **blocks the main thread**, leading to performance issues.

---
By understanding `runBlocking`, you can effectively control coroutine execution and ensure smooth interoperability between blocking and non-blocking code.
