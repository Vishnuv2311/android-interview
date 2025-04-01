# How to Run Parallel Tasks and Get a Callback When All Are Complete

In Kotlin, you can use coroutines to run parallel tasks and get a callback when all are complete. This can be done using `async` and `awaitAll` from `kotlinx.coroutines`.

## Example using `coroutineScope`
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    println("Starting parallel tasks...")

    val results = coroutineScope {
        val task1 = async { fetchDataFromNetwork() }
        val task2 = async { processData() }
        val task3 = async { performComputation() }
        listOf(task1, task2, task3).awaitAll()
    }

    println("All tasks completed with results: $results")
}

suspend fun fetchDataFromNetwork(): String {
    delay(2000)
    return "Network Data"
}

suspend fun processData(): String {
    delay(1000)
    return "Processed Data"
}

suspend fun performComputation(): String {
    delay(1500)
    return "Computation Result"
}
```

## Explanation:
1. `async` launches the tasks in parallel.
2. `awaitAll()` waits for all tasks to complete.
3. When all tasks are done, we get a callback with their results.

This method ensures efficient execution and optimal resource utilization.
