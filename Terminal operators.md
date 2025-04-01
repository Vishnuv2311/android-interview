# Kotlin Flow Terminal Operators

## Overview  
Terminal operators in Kotlin Flow are functions that **collect, transform, or reduce** the emitted values and **trigger the execution of the Flow**. These operators are **always at the end** of a Flow chain.

---

## 🔹 List of Terminal Operators  

| Operator | Description | Example Use Case |
|----------|-------------|------------------|
| `collect()` | Collects and processes each emitted value, allowing side effects like logging or updating UI. | Printing values from a Flow |
| `collectLatest()` | Cancels previous collection if a new value arrives, useful for scenarios where only the latest value matters. | Real-time search queries |
| `toList()` | Collects all emitted values into a list, enabling batch processing of results. | Storing API responses in a list |
| `toSet()` | Collects all unique emitted values into a set, ensuring no duplicates are retained. | Removing duplicates from a Flow |
| `first()` | Returns the first emitted value, useful for scenarios where only the initial value is needed. | Fetching the first available item |
| `firstOrNull()` | Returns the first value or `null` if empty, providing a safe way to handle empty flows. | Handling empty Flow scenarios |
| `single()` | Returns the only emitted value, throws an error if more than one value is emitted, ensuring singularity. | Ensuring a Flow has exactly one item |
| `singleOrNull()` | Returns the only emitted value or `null` if empty, allowing safe retrieval of a single item. | Fetching a single item safely |
| `reduce()` | Combines emitted values to return a single result, typically used for calculations. | Calculating sum or concatenation |
| `fold()` | Similar to `reduce()`, but allows specifying an initial value, providing more control over the accumulation. | Summing numbers with a starting value |
| `launchIn()` | Collects Flow inside a CoroutineScope, facilitating the integration of Flow with coroutines. | Running Flow in `lifecycleScope` |

---

## 📌 Examples  

### 1️⃣ **`collect()` – Collecting Emitted Values**  
The `collect()` operator is used to gather and process each emitted value from a Flow.  

```kotlin
val numberFlow = flowOf(1, 2, 3)

numberFlow.collect { value ->
    println("Received: $value")
}
```

✅ Output:

Received: 1  
Received: 2  
Received: 3  

---

### 2️⃣ **`collectLatest()` – Only Keeping the Latest Value**  
The `collectLatest()` operator is useful when you want to cancel the previous collection if a new value arrives, ensuring only the most recent value is processed.  

```kotlin
numberFlow.collectLatest { value ->
    println("Collecting: $value")
    delay(500)  // Simulating work
}
```

✅ Output: (Previous values may be skipped if a new one arrives)

Collecting: 1  
Collecting: 2  
Collecting: 3  

---

### 3️⃣ **`toList()` – Collecting Flow as a List**  
The `toList()` operator collects all emitted values into a list, making it easy to work with the entire set of results.  

```kotlin
val list = numberFlow.toList()
println(list)
```

✅ Output:

[1, 2, 3]  

---

### 4️⃣ **`first()` – Fetching Only the First Item**  
The `first()` operator retrieves the first emitted value from a Flow, which is useful when you only need the initial item.  

```kotlin
val firstValue = numberFlow.first()
println(firstValue)
```

✅ Output:

1  

---

### 5️⃣ **`reduce()` – Summing Up Flow Values**  
The `reduce()` operator combines all emitted values to produce a single result, often used for calculations like sums.  

```kotlin
val sum = numberFlow.reduce { acc, value -> acc + value }
println(sum)
```

✅ Output:

6  

📌 Explanation: 1 + 2 + 3 = 6  

---

### 6️⃣ **`fold()` – Summing with an Initial Value**  
The `fold()` operator works similarly to `reduce()`, but allows you to specify an initial value for accumulation.  

```kotlin
val sumWithStart = numberFlow.fold(10) { acc, value -> acc + value }
println(sumWithStart)
```

✅ Output:

16  

📌 Explanation: 10 (start) + 1 + 2 + 3 = 16  

---

### 7️⃣ **`launchIn()` – Running Flow in a Scope**  
The `launchIn()` operator is used to collect a Flow within a specified CoroutineScope, facilitating coroutine integration.  

```kotlin
val scope = CoroutineScope(Dispatchers.Main)
numberFlow.onEach { println(it) }
    .launchIn(scope)
```

✅ Runs the Flow inside the provided CoroutineScope.  

---

🎯 Summary
- Terminal operators trigger the execution of Flow.
- Use `collect()` to process each emitted value.
- Use `reduce()` or `fold()` for accumulating results.
- Use `first()`, `single()`, or `toList()` for retrieving specific items.

---

📌 When to Use?

| Scenario | Best Terminal Operator |
|----------|-----------------------|
| Print each value from Flow | `collect()` |
| Only get the first item | `first()` |
| Convert Flow to List | `toList()` |
| Process only the latest value | `collectLatest()` |
| Sum values in Flow | `reduce()` or `fold()` |
