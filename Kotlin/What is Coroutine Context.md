# What is Coroutine Context in Kotlin?

Coroutine Context in Kotlin is a set of elements that define the behavior of a coroutine. It consists of several key components, including:

### Components of Coroutine Context:
1. **Job** – Defines the lifecycle of the coroutine.
2. **Dispatcher** – Determines the thread on which the coroutine runs.
3. **Coroutine Name** – Assigns a name to the coroutine for debugging.
4. **CoroutineExceptionHandler** – Handles uncaught exceptions in coroutines.

### Example:
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val coroutineContextExample = launch(Dispatchers.IO + CoroutineName("ExampleCoroutine")) {
        println("Running in coroutine: ${coroutineContext[CoroutineName]}")
    }
    coroutineContextExample.join()
}
```

### Key Points:
- `Dispatchers.Main` – Runs on the main thread (Android UI operations).
- `Dispatchers.IO` – Optimized for disk and network operations.
- `Dispatchers.Default` – Optimized for CPU-intensive tasks.
- `Job` – Allows cancellation and tracking of coroutine lifecycle.
- `CoroutineExceptionHandler` – Handles exceptions globally.

Coroutine Context allows coroutines to execute efficiently by managing their behavior, execution thread, and lifecycle.
