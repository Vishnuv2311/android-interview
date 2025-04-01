# What is the Meaning of Structured Concurrency in Kotlin Coroutines?

Structured concurrency in Kotlin Coroutines is a programming paradigm that ensures that coroutines are executed within a defined scope, preventing resource leaks and making cancellation predictable. It allows coroutines to be properly managed and ensures that all child coroutines complete before their parent coroutine finishes.

## Key Concepts of Structured Concurrency:

1. **Coroutine Scope** - All coroutines must run within a specific scope (e.g., `GlobalScope`, `lifecycleScope`, or `viewModelScope`). This ensures coroutines do not outlive their intended lifecycle.

2. **Hierarchy of Coroutines** - Child coroutines inherit the context of their parent coroutine. If a parent coroutine is canceled, all its child coroutines are also canceled automatically.

3. **Automatic Cancellation** - If an error occurs in a child coroutine, it propagates to its parent, which can handle the error and ensure proper cleanup.

4. **Job and SupervisorJob** - `Job` helps in tracking coroutine completion, and `SupervisorJob` allows child coroutines to fail independently without canceling siblings.

## Example of Structured Concurrency:

```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val parentJob = launch {
        launch {
            delay(1000)
            println("Child coroutine 1 completed")
        }
        launch {
            delay(500)
            println("Child coroutine 2 completed")
        }
    }
    parentJob.join()
    println("Parent coroutine completed")
}
```

### Benefits of Structured Concurrency:
- Prevents memory leaks
- Ensures predictable lifecycle management
- Makes coroutine cancellation easier to handle
- Reduces the risk of orphaned coroutines

Structured concurrency is a key concept in Kotlin Coroutines that enhances the maintainability and reliability of concurrent programming.
