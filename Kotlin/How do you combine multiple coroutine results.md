# How to Combine Multiple Coroutine Results in Kotlin

When working with coroutines in Kotlin, you often need to combine multiple results efficiently. There are different ways to achieve this based on the use case:

## 1. Using `async` and `awaitAll`
The `async` builder allows running multiple coroutines concurrently, and `awaitAll` can be used to await their completion.

```kotlin
import kotlinx.coroutines.*

suspend fun fetchData1(): String {
    delay(1000)
    return "Result 1"
}

suspend fun fetchData2(): String {
    delay(1500)
    return "Result 2"
}

fun main() = runBlocking {
    val result = coroutineScope {
        val deferred1 = async { fetchData1() }
        val deferred2 = async { fetchData2() }
        listOf(deferred1.await(), deferred2.await())
    }
    println(result) // Output: [Result 1, Result 2]
}
```

## 2. Using `zip` Operator with Flow
If working with `Flow`, you can use the `zip` operator to combine results as they arrive.

```kotlin
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.runBlocking

fun flow1() = flow {
    emit("A")
    delay(1000)
    emit("B")
}

fun flow2() = flow {
    emit(1)
    delay(1500)
    emit(2)
}

fun main() = runBlocking {
    flow1().zip(flow2()) { a, b -> "$a$b" }.collect { println(it) }
}
```

### 3. Using `combine` for Real-Time Updates
When multiple `StateFlow` or `SharedFlow` values need to be combined dynamically, use `combine`.

```kotlin
val flow1 = MutableStateFlow("Hello")
val flow2 = MutableStateFlow("World")

val combinedFlow = flow1.combine(flow2) { f1, f2 -> "$f1 $f2" }
```

## Choosing the Right Method
- Use `async/awaitAll` for simple concurrent tasks.
- Use `zip` for pairing emitted items.
- Use `combine` for merging state updates dynamically.

Each method serves different use cases depending on performance needs and concurrency control.
