# 🔄 StateFlow vs SharedFlow vs callbackFlow vs channelFlow in Kotlin

## 📌 Overview  
Kotlin provides multiple **Hot Flow** and **Channel** alternatives to handle **asynchronous data streams** efficiently. This document explains **StateFlow**, **SharedFlow**, **callbackFlow**, and **channelFlow** with key differences and use cases.

---

## **1️⃣ StateFlow: UI State Holder (Hot Flow)**
### ✅ Characteristics  
- **Holds the latest value** and always emits it to new collectors.  
- Always requires an **initial value**.  
- **Emits only when value changes** (avoids unnecessary updates).  
- Used for **state management** in **ViewModel** (similar to `LiveData`).  

### 🔹 Example: `StateFlow`  
```kotlin
val _stateFlow = MutableStateFlow(0)  // Requires initial value
val stateFlow: StateFlow<Int> = _stateFlow

fun main() = runBlocking {
    launch {
        repeat(5) {
            delay(500)
            _stateFlow.value = it  // Updating the flow value
        }
    }

    delay(1000)  // Collector starts late
    stateFlow.collect { println("Collector received: $it") }
}
```

✅ **Output:**
```
Collector received: 2
Collector received: 3
Collector received: 4
```

📌 **New collectors only get the latest emitted value.**  

---

## **2️⃣ SharedFlow: Multi-Consumer Event Stream (Hot Flow)**

### ✅ Characteristics
- **Does NOT require an initial value.**
- **Can replay previous values** to new collectors.
- **Supports multiple consumers**, like an event bus.
- Used for **one-time events, notifications, and messages.**

### 🔹 Example: `SharedFlow`
```kotlin
val _sharedFlow = MutableSharedFlow<Int>(replay = 2)  // Stores last 2 values
val sharedFlow: SharedFlow<Int> = _sharedFlow

fun main() = runBlocking {
    launch {
        repeat(5) {
            delay(500)
            _sharedFlow.emit(it)  // Emits values
        }
    }

    delay(1200)  // Collector starts late
    sharedFlow.collect { println("Collector received: $it") }
}
```

✅ **Output:**
```
Collector received: 2
Collector received: 3
Collector received: 4
```

📌 **Replays the last 2 values to new collectors.**

---

## **3️⃣ callbackFlow: Convert Callbacks to Flow**

### ✅ Characteristics
- **Used to convert callback-based APIs into Flow.**
- **Supports suspension and cancellation.**
- Must call `trySend()` instead of `emit()`.
- Commonly used for **location updates, sensor data, network callbacks**.

### 🔹 Example: `callbackFlow`
```kotlin
fun locationUpdates(): Flow<String> = callbackFlow {
    val listener = object : LocationListener {
        override fun onLocationChanged(location: String) {
            trySend(location)  // Use trySend() instead of emit()
        }
    }
    addLocationListener(listener)
    
    awaitClose { removeLocationListener(listener) }  // Clean up when cancelled
}
```

📌 **Automatically cancels when the collector stops listening.**

---

## **4️⃣ channelFlow: More Flexible Callback Flow**

### ✅ Characteristics
- **Similar to `callbackFlow` but allows buffering multiple values.**
- **Better for multi-threaded environments.**
- Uses `send()` instead of `emit()`.

### 🔹 Example: `channelFlow`
```kotlin
fun sensorData(): Flow<Int> = channelFlow {
    launch {
        repeat(5) {
            send(it)  // Sends data
            delay(500)
        }
    }
}
```

📌 **More flexible than `callbackFlow` for multi-threading.**

---

## **5️⃣ Key Differences: StateFlow vs SharedFlow vs callbackFlow vs channelFlow**

| Feature              | StateFlow | SharedFlow | callbackFlow | channelFlow |
|----------------------|----------|------------|--------------|-------------|
| **Cold/Hot**        | Hot      | Hot        | Hot          | Hot         |
| **Requires Initial Value?** | ✅ Yes | ❌ No | ❌ No | ❌ No |
| **Replays Old Values?** | ✅ Always latest | ✅ Configurable | ❌ No | ❌ No |
| **Multiple Collectors?** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Use Case** | UI State (LiveData alternative) | Events, Notifications | Converting Callbacks to Flow | Background Multi-threaded Data |

---

## **6️⃣ When to Use Which?**

| Scenario                           | StateFlow | SharedFlow | callbackFlow | channelFlow |
|-------------------------------------|----------|------------|--------------|-------------|
| UI State Management (ViewModel)    | ✅ Yes   | ❌ No      | ❌ No        | ❌ No       |
| Event Bus (Multiple Consumers)     | ❌ No    | ✅ Yes     | ❌ No        | ❌ No       |
| Location Updates (Callbacks)       | ❌ No    | ❌ No      | ✅ Yes       | ✅ Yes      |
| Sensor Data Streaming              | ❌ No    | ❌ No      | ❌ No        | ✅ Yes      |

---

## **📌 Summary**

- ✅ **StateFlow** is best for **state management** (similar to LiveData).
- ✅ **SharedFlow** is best for **event-driven programming** with multiple collectors.
- ✅ **callbackFlow** is best for **converting callback-based APIs to Flow**.
- ✅ **channelFlow** is best for **multi-threaded data streaming**.
