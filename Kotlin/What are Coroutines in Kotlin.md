# What are Coroutines in Kotlin?

Kotlin Coroutines are a way to handle asynchronous programming efficiently. They allow you to write non-blocking, concurrent code in a sequential manner, making it easier to read and maintain.

## Key Features of Coroutines:

- **Lightweight**: Coroutines are more efficient than threads as they don't require a separate OS thread.
- **Suspending Functions**: Functions marked with `suspend` can be paused and resumed later without blocking the thread.
- **Structured Concurrency**: Coroutines are managed within a defined scope to prevent memory leaks and ensure proper execution.
- **Built-in Dispatchers**: Provides control over which thread a coroutine runs on (e.g., `Dispatchers.IO`, `Dispatchers.Main`).
- **Exception Handling**: Offers structured error handling with `try-catch`, `CoroutineExceptionHandler`, etc.

## Example:

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    launch {
        delay(1000L)
        println("Coroutine executed after 1 second")
    }
    println("Main function continues")
}
```

### Benefits of Using Coroutines:
- Avoids callback hell
- Improves performance by avoiding thread blocking
- Simplifies writing asynchronous code

### Common Coroutine Builders:
- `launch` - Fire and forget (returns `Job`)
- `async` - Returns a `Deferred` result
- `runBlocking` - Blocks the thread until execution is complete

Coroutines make Kotlin's asynchronous programming more manageable, improving code clarity and performance.
