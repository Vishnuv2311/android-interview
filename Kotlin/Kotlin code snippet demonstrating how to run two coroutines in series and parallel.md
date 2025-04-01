### Running Two Coroutines in Series and Parallel in Kotlin

#### Running Coroutines in Series
```kotlin
import kotlinx.coroutines.*

suspend fun task1(): String {
    delay(1000) // Simulating work
    return "Task 1 Completed"
}

suspend fun task2(): String {
    delay(1000) // Simulating work
    return "Task 2 Completed"
}

fun main() = runBlocking {
    val result1 = task1()
    println(result1)
    
    val result2 = task2()
    println(result2)
}
```

#### Running Coroutines in Parallel
```kotlin
import kotlinx.coroutines.*

suspend fun task1(): String {
    delay(1000) // Simulating work
    return "Task 1 Completed"
}

suspend fun task2(): String {
    delay(1000) // Simulating work
    return "Task 2 Completed"
}

fun main() = runBlocking {
    val deferred1 = async { task1() }
    val deferred2 = async { task2() }
    
    println(deferred1.await())
    println(deferred2.await())
}
```

### Explanation
- **Series Execution**: The second coroutine starts only after the first one completes.
- **Parallel Execution**: Both coroutines start simultaneously using `async`, improving efficiency.
