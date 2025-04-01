# Suspending vs Blocking in Kotlin Coroutines

In Kotlin coroutines, the key difference between **suspending** and **blocking** is how they handle thread execution:

## Suspending
- A **suspending function** does not block the thread but **pauses execution** and allows other work to run on the same thread.
- It is marked with the `suspend` keyword.
- Uses cooperative multitasking to avoid thread blocking.
- Example:
    ```kotlin
    suspend fun fetchData() {
        delay(1000) // Suspends the coroutine without blocking the thread
        println("Data fetched")
    }
    ```

## Blocking
- A **blocking call** holds the thread execution, preventing other tasks from using it.
- Uses traditional thread-based operations like `Thread.sleep()`.
- Can lead to inefficiencies if used inside coroutines.
- Example:
    ```kotlin
    fun fetchDataBlocking() {
        Thread.sleep(1000) // Blocks the thread
        println("Data fetched")
    }
    ```

## Key Differences

| Feature          | Suspending                    | Blocking                     |
|-----------------|--------------------------------|------------------------------|
| Thread Usage    | Does not block threads        | Blocks the thread execution |
| Efficiency      | More efficient in coroutines | Less efficient due to thread holding |
| Function Type   | `suspend fun`                 | Regular function            |

## Best Practices
- Prefer **suspending functions** inside coroutines to avoid blocking the main thread.
- Use `withContext(Dispatchers.IO)` when performing blocking operations in coroutines.
- Avoid calling blocking functions inside coroutine scopes to maintain efficiency.
