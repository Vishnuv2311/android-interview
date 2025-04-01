# 🚀 Creating Flow Using Flow Builder in Kotlin

## 📌 Overview  
In Kotlin, **Flow Builder** functions are used to **create** and **emit** values asynchronously as a Flow. These builders allow us to generate a **Cold Flow**, which starts emitting only when collected.

---

## **1️⃣ Types of Flow Builders**  
Kotlin provides several ways to create Flows:

| Flow Builder    | Description                                      | Use Case                   |
|----------------|--------------------------------------------------|----------------------------|
| `flow {}`      | Creates a Flow that emits multiple values asynchronously | API calls, database queries |
| `flowOf()`     | Creates a Flow from a fixed set of values        | Static data                |
| `asFlow()`     | Converts collections or sequences into a Flow     | Transform lists to Flow    |
| `channelFlow()` | Allows concurrent emission from multiple coroutines | Multi-threaded data emission |

---

## **2️⃣ `flow {}` – The Standard Flow Builder**
The `flow {}` builder is the **most flexible** way to create a Flow. It allows **emitting values** inside a suspending block.

### 🔹 Example: Creating a Flow Using `flow {}`
```kotlin
val numberFlow = flow {
    println("Flow started")  // Executes only when collected
    for (i in 1..3) {
        delay(1000)  // Simulating async work
        emit(i)  // Emitting values
    }
}

// Collecting the flow
runBlocking {
    numberFlow.collect { value -> println("Received: $value") }
}
```

✅ **Output (when collected):**
```
Flow started
Received: 1
Received: 2
Received: 3
```

---

## **3️⃣ `flowOf()` – Creating a Flow from Static Values**
The `flowOf()` function is useful when you have a **fixed set of values**.

### 🔹 Example: `flowOf()`
```kotlin
val staticFlow = flowOf("A", "B", "C")

runBlocking {
    staticFlow.collect { println(it) }
}
```

✅ **Output:**
```
A
B
C
```

📌 Each item is emitted one by one.

---

## **4️⃣ `asFlow()` – Converting a Collection to Flow**
The `asFlow()` function is used to **transform collections** into a Flow.

### 🔹 Example: `asFlow()`
```kotlin
val listFlow = listOf(10, 20, 30).asFlow()

runBlocking {
    listFlow.collect { println(it) }
}
```

✅ **Output:**
```
10
20
30
```

---

## **5️⃣ `channelFlow()` – More Flexible Flow with Multi-threading**
The `channelFlow()` builder allows **concurrent emission** from multiple coroutines.

### 🔹 Example: `channelFlow()`
```kotlin
val channelFlow = channelFlow {
    launch { send(1) }
    launch { send(2) }
}

runBlocking {
    channelFlow.collect { println(it) }
}
```

✅ **Output (order may vary due to concurrency):**
```
1
2
```

---

## **📌 Summary**
- ✅ `flow {}` – Best for **async data generation** (supports suspending functions).
- ✅ `flowOf()` – Best for **static values** (predefined set of elements).
- ✅ `asFlow()` – Best for **converting collections** to Flow.
- ✅ `channelFlow()` – Best for **multi-threaded emission**.
