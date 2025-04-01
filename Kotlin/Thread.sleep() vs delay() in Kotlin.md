# Thread.sleep() vs delay() in Kotlin

## 1. Thread.sleep()
- `Thread.sleep(milliseconds)` is a blocking function that pauses the current thread for the specified duration.
- It blocks the entire thread, meaning no other tasks can run on that thread until the sleep duration is over.
- Used in traditional multi-threading.

### Example:
```kotlin
fun main() {
    println("Before sleep")
    Thread.sleep(2000) // Blocks the thread for 2 seconds
    println("After sleep")
}
```

## 2. delay()
- `delay(milliseconds)` is a suspending function used in Kotlin Coroutines.
- Unlike `Thread.sleep()`, it does **not** block the thread but suspends the coroutine, allowing other coroutines to run in the meantime.
- Used in coroutine-based asynchronous programming.

### Example:
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    println("Before delay")
    delay(2000) // Suspends the coroutine without blocking the thread
    println("After delay")
}
```

## 3. Key Differences

| Feature         | `Thread.sleep()` | `delay()` |
|----------------|----------------|-----------|
| Type          | Blocking | Suspending (Non-blocking) |
| Thread Impact | Blocks the thread | Only suspends the coroutine |
| Used In      | Traditional threads | Kotlin Coroutines |
| Parallel Execution | No, it halts execution | Yes, allows other coroutines to execute |

## 4. When to Use What?
- Use `Thread.sleep()` in traditional multi-threaded applications.
- Use `delay()` when working with Kotlin Coroutines to prevent blocking the main thread.
