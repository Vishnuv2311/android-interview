# ⚠️ Exception Handling in Kotlin Flow  

## 📌 Overview  
Exception handling in **Kotlin Flow** ensures that **errors do not crash the app** and can be gracefully handled. Kotlin Flow provides multiple operators for handling exceptions, including:  
✔ **`catch()`** – Catches and processes exceptions inside the Flow.  
✔ **`onEach {}`** – Handles logging/debugging without stopping the Flow.  
✔ **`retry()`** – Retries the Flow when an exception occurs.  
✔ **`retryWhen()`** – Retries with conditions, adding delay between retries.  

---

## **1️⃣ Handling Exceptions with `catch()`**
### ✅ Characteristics  
✔ **Catches exceptions in Flow** and allows recovery.  
✔ **Must be placed before `collect()`**.  

### 🔹 Example: Using `catch()`
```kotlin
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.runBlocking

fun getNumbers(): Flow<Int> = flow {
    emit(1)
    emit(2)
    throw RuntimeException("Something went wrong!")  // Simulating an error
    emit(3)  // ❌ Will not be emitted
}

fun main() = runBlocking {
    getNumbers()
        .catch { e -> println("Caught exception: ${e.message}") }
        .collect { println("Received: $it") }
}
```
✅ **Output:**
```
Received: 1
Received: 2
Caught exception: Something went wrong!
```
📌 `catch()` prevents Flow from crashing.

---

### 2️⃣ Using `catch()` for Default Values  
If an error occurs, we can emit a fallback value instead of stopping the Flow.
```kotlin
getNumbers()
    .catch { e -> emit(-1) }  // Emits -1 on error
    .collect { println("Received: $it") }
```
✅ **Output:**
```
Received: 1
Received: 2
Received: -1  // Error handled with fallback value
```

---

### 3️⃣ Using `onEach {}` for Logging Errors  
- `onEach()` logs values but does not handle exceptions.  
- `catch()` is still required to prevent the Flow from stopping.  
```kotlin
getNumbers()
    .onEach { println("Processing: $it") }
    .catch { e -> println("Error: ${e.message}") }
    .collect()
```
✅ **Output:**
```
Processing: 1
Processing: 2
Error: Something went wrong!
```
📌 Best for debugging/logging purposes.

---

### 4️⃣ Retrying Failed Flow with `retry()`  
- Retries the Flow automatically when an error occurs.  
- Can specify the number of retries.  
```kotlin
getNumbers()
    .retry(3)  // Retries up to 3 times before failing
    .catch { e -> println("Final failure: ${e.message}") }
    .collect()
```
📌 Great for handling transient failures like network errors.

---

### 5️⃣ Adding Delay Between Retries with `retryWhen()`  
- Retries conditionally based on the exception type.  
- Allows adding a delay between retries.  
```kotlin
getNumbers()
    .retryWhen { cause, attempt ->
        if (attempt < 3) {  // Retry only 3 times
            println("Retrying attempt: $attempt")
            delay(1000)  // Wait 1 second before retrying
            true
        } else {
            false  // Stop retrying
        }
    }
    .catch { e -> println("Final error: ${e.message}") }
    .collect()
```
✅ **Output:**
```
Retrying attempt: 0
Retrying attempt: 1
Retrying attempt: 2
Final error: Something went wrong!
```
📌 Useful for implementing backoff strategies.

---

## **6️⃣ Summary: Best Practices for Exception Handling**
| Operator     | Use Case |
|--------------|----------|
| **catch()**  | Handles errors inside Flow and allows recovery with fallback values. |
| **onEach()** | Logs/debugs without stopping the Flow. |
| **retry(n)** | Retries the Flow `n` times when an error occurs. |
| **retryWhen()** | Adds conditional retries with delays. |

---

## 📌 Final Thoughts  
✔ Use `catch()` to gracefully handle errors inside Flow.  
✔ Use `retry()` or `retryWhen()` for transient failures (e.g., API calls).  
✔ Log errors with `onEach()` without stopping execution.  
✔ Always place `catch()` before `collect()` to properly catch exceptions.  
