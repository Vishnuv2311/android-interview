# 🔹 `lateinit` vs `lazy` in Kotlin

## 📌 Overview  
Both **`lateinit`** and **`lazy`** are used for **delayed initialization** in Kotlin, but they have different use cases and behaviors.

---

## **1️⃣ Key Differences**

| Feature | `lateinit` | `lazy` |
|---------|-----------|--------|
| **Variable Type** | `var` (Mutable) | `val` (Immutable) |
| **Initialization Time** | Set **later** in the lifecycle | First **access time** |
| **Data Type Support** | Any non-nullable type (excluding primitives) | Any data type |
| **Thread Safety** | ❌ Not thread-safe | ✅ Thread-safe by default |
| **Usage** | Used when a variable is assigned **before use** (e.g., dependency injection, UI elements) | Used for **expensive computations** that should only run when needed |

---

## **2️⃣ `lateinit` – Used for Mutable Variables**  
- Works with **`var`** (mutable).  
- Used when initialization **must happen before usage** but **cannot be done at declaration**.  
- Typically used for **dependency injection, Android views, and non-nullable properties**.

### ✅ **Example: Using `lateinit` in an Android Activity**  
```kotlin
class MainActivity : AppCompatActivity() {
    lateinit var textView: TextView  // No need to initialize here

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        textView = findViewById(R.id.textView)  // Initialized later
        textView.text = "Hello, Kotlin!"
    }
}
```
📌 **Avoids using nullable properties (`?`) for UI components.**  

### 🔹 **Checking If `lateinit` Variable Is Initialized**
```kotlin
if (::textView.isInitialized) {
    println("TextView is initialized")
}
```
📌 **Prevents `UninitializedPropertyAccessException`.**  

---

## **3️⃣ `lazy` – Used for Immutable Variables**  
- Works with **`val`** (immutable).  
- Used when a value **should be computed only when accessed**.  
- Typically used for **expensive operations (e.g., database queries, API calls).**

### ✅ **Example: Using `lazy` for Expensive Computation**  
```kotlin
val heavyComputation: String by lazy {
    println("Computing value...")
    "Result of Computation"
}

fun main() {
    println("Before Accessing lazy property")
    println(heavyComputation)  // First call triggers computation
    println(heavyComputation)  // Second call reuses computed value
}
```
✅ **Output:**  
```
Before Accessing lazy property
Computing value...
Result of Computation
Result of Computation
```
📌 **The value is computed only once and reused.**  

---

## **4️⃣ When to Use `lateinit` vs `lazy`?**

| Scenario | Best Choice |
|----------|------------|
| **UI components in Android** | `lateinit` |
| **Expensive computations (e.g., API calls, database queries)** | `lazy` |
| **Dependency injection** | `lateinit` |
| **Properties that must be initialized before use** | `lateinit` |
| **Thread-safe initialization** | `lazy` |
| **Immutable properties** | `lazy` |

---

## **📌 Summary**  
✅ **Use `lateinit` for `var` (mutable) properties that will be initialized before use.**  
✅ **Use `lazy` for `val` (immutable) properties that should be computed only when needed.**  
✅ **Avoid `lateinit` with primitive types (`Int`, `Boolean`, etc.).**  
✅ **Use `lazy` for thread-safe initialization and expensive operations.**  

