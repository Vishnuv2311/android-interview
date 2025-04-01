# Launch vs Async in Kotlin Coroutines

Kotlin Coroutines provide `launch` and `async` builders to run tasks concurrently, but they serve different purposes.

## **1. launch**
- Used to start a coroutine that does not return a result.
- Returns a `Job` that can be used to track and cancel the coroutine.
- Suitable for fire-and-forget tasks.

### **Example:**
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val job = launch {
        delay(1000L)
        println("Task completed")
    }
    println("Waiting...")
    job.join() // Wait for completion
}
```

## **2. async**
- Used to start a coroutine that returns a result.
- Returns a `Deferred<T>` that can be awaited using `.await()`.
- Suitable for parallel computations.

### **Example:**
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val deferred = async {
        delay(1000L)
        "Result"
    }
    println("Waiting for result...")
    println("Received: ${deferred.await()}") // Waits and gets the result
}
```

## **Key Differences**
| Feature  | launch | async |
|----------|--------|-------|
| Return Type | Job | Deferred<T> |
| Purpose | Fire-and-forget tasks | Returns a result |
| Cancellation | Can be cancelled using `job.cancel()` | Can be cancelled using `deferred.cancel()` |
| Awaiting Completion | Uses `join()` | Uses `await()` |

## **When to Use Which?**
- Use `launch` when you don’t need a result and just want to execute a coroutine.
- Use `async` when you need a result from the coroutine.
