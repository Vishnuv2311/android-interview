# 🔄 Retry Operator in Kotlin Flow  

## 📌 Overview  
The **`retry` operator** in Kotlin Flow allows you to **automatically retry a failed Flow multiple times** before giving up. This is particularly useful for handling **transient failures** such as **network errors, API timeouts, or database failures**.  

---

## **1️⃣ How Does `retry` Work?**  
- **Retries the Flow automatically when an exception occurs.**  
- **Stops retrying once the retry limit is reached.**  
- **Can include a condition to decide when to retry.**  

---

## **2️⃣ Basic Example: Retrying a Failed Flow**  

```kotlin
val flowWithRetry = flow {
    emit(1)
    throw RuntimeException("Error occurred!")  // Simulating an error
}.retry(3)  // Retries up to 3 times
    .catch { println("Failed after retries: ${it.message}") }
    .collect { println("Received: $it") }
```

### ✅ Output:
```
Received: 1
Received: 1
Received: 1
Received: 1
Failed after retries: Error occurred!
```

**📌 Explanation:**  
- The Flow retries **three times** before finally failing.

---

## **3️⃣ Using `retry` with a Condition**  

You can retry only for specific exceptions using a **predicate condition**.

```kotlin
val flowWithConditionalRetry = flow {
    emit(1)
    throw IllegalStateException("Retryable error!")  // Simulating error
}.retry(3) { cause -> cause is IllegalStateException }  // Retries only for `IllegalStateException`
    .catch { println("Final Failure: ${it.message}") }
    .collect { println("Received: $it") }
```

### ✅ Behavior:
- The Flow **retries only for `IllegalStateException`** but **not for other exceptions**.

---

## **4️⃣ Adding a Delay Between Retries with `retryWhen`**  

The **`retryWhen`** operator allows you to add a **delay before retrying**.

```kotlin
val flowWithDelayRetry = flow {
    emit(1)
    throw RuntimeException("Temporary error!")
}.retryWhen { cause, attempt ->
    if (attempt < 3) {  // Retry up to 3 times
        delay(1000)  // Wait 1 second before retrying
        println("Retrying... attempt $attempt")
        true
    } else {
        false  // Stop retrying after 3 attempts
    }
}.catch { println("Final Failure: ${it.message}") }
.collect { println("Received: $it") }
```

### ✅ Output:
```
Received: 1
Retrying... attempt 0
Received: 1
Retrying... attempt 1
Received: 1
Retrying... attempt 2
Received: 1
Final Failure: Temporary error!
```

**📌 Explanation:**  
- Retries happen **with a delay** and **stop after 3 attempts**.

---

## **5️⃣ `retry` vs `retryWhen`**

| Feature           | `retry()` | `retryWhen()` |
|------------------|-----------|----------------|
| Retries automatically? | ✅ Yes | ✅ Yes |
| Can specify exception type? | ✅ Yes | ✅ Yes |
| Can include a delay? | ❌ No | ✅ Yes |
| Can decide based on attempt count? | ❌ No | ✅ Yes |

---

## **6️⃣ When to Use `retry`?**

| Scenario | Use `retry()` | Use `retryWhen()` |
|----------|---------------|------------------|
| Network request failures | ✅ Yes | ✅ Yes |
| Database query failures | ✅ Yes | ✅ Yes |
| Adding delay between retries | ❌ No | ✅ Yes |
| Stopping retries after N attempts | ❌ No | ✅ Yes |

---

## **📌 Summary**
- **Use `retry()`** to **retry failed Flows automatically**.
- **Use `retryWhen()`** for **conditional retries with delays**.
- **Retry only for specific exceptions** using a **predicate function**.
- **Helpful for handling network/API failures gracefully**.
