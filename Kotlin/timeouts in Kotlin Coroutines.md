# Timeouts in Kotlin Coroutines

In Kotlin Coroutines, timeouts help in canceling long-running operations if they exceed a certain duration. This is useful to avoid blocking resources indefinitely.

## Using `withTimeout`
`withTimeout` cancels the coroutine if it runs longer than the specified time.

### Example:
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    try {
        withTimeout(2000) {
            repeat(5) {
                println("Working...")
                delay(1000)
            }
        }
    } catch (e: TimeoutCancellationException) {
        println("Timeout occurred: ${e.message}")
    }
}
```
### Output:
```
Working...
Working...
Timeout occurred: Timed out waiting for 2000 ms
```

## Using `withTimeoutOrNull`
`withTimeoutOrNull` is similar but returns `null` instead of throwing an exception.

### Example:
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val result = withTimeoutOrNull(2000) {
        repeat(5) {
            println("Processing...")
            delay(1000)
        }
        "Completed"
    }
    println(result ?: "Timed out")
}
```
### Output:
```
Processing...
Processing...
Timed out
```

## Key Differences
| Feature | `withTimeout` | `withTimeoutOrNull` |
|---------|--------------|--------------------|
| Behavior | Throws `TimeoutCancellationException` | Returns `null` |
| Use Case | When timeout failure should be handled via exception | When failure should return a default value |

Using timeouts effectively ensures that your application remains responsive and does not hang due to long-running operations.
