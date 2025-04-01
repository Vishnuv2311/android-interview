# 🔹 When to Use `lateinit` Keyword in Kotlin?  

## 📌 Overview  
The **`lateinit`** keyword in Kotlin is used for **delayed initialization** of **mutable (`var`) non-nullable properties**. It is useful when a property **cannot be initialized at declaration** but **will be assigned before use**.

---

## **1️⃣ Why Use `lateinit`?**  
| Feature | Benefit |
|---------|---------|
| **Delays initialization** | Avoids unnecessary object creation at startup. |
| **No need for nullable types** | Prevents using `null` and `?.` operators. |
| **Improves performance** | Avoids unnecessary memory allocation. |

---

## **2️⃣ How to Use `lateinit`?**
### ✅ **Basic Syntax**
```kotlin
class User {
    lateinit var name: String  // Declared but not initialized
}

📌 Must be mutable (var), and cannot be val.

⸻

3️⃣ When to Use lateinit?

Use Case	Should Use lateinit?
Dependency Injection	✅ Yes
Initializing Views in Android	✅ Yes
Variables assigned later (e.g., onCreate())	✅ Yes
Primitive Data Types (Int, Boolean, etc.)	❌ No
Immutable (val) variables	❌ No



⸻

4️⃣ Example: Initializing Views in Android

class MainActivity : AppCompatActivity() {
    lateinit var textView: TextView  // View initialized later

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        textView = findViewById(R.id.textView)  // Initialized here
        textView.text = "Hello Kotlin!"
    }
}

📌 Avoids using nullable types (?) for UI components.

⸻

5️⃣ Checking If lateinit Variable Is Initialized

Use ::variable.isInitialized to check before accessing it.

if (::name.isInitialized) {
    println("Name is: $name")
} else {
    println("Name is not initialized")
}

📌 Prevents UninitializedPropertyAccessException.

⸻

6️⃣ lateinit vs lazy

Feature	lateinit var	lazy val
Usage	Mutable (var)	Immutable (val)
Initialization	Done later in lifecycle	Initialized when first accessed
Thread Safety	❌ No	✅ Yes



⸻

📌 Summary

✅ Use lateinit for non-nullable, mutable (var) properties.
✅ Best for Dependency Injection, UI components, and variables assigned later.
✅ Use ::var.isInitialized before accessing to avoid crashes.
✅ Do NOT use with primitive types (Int, Boolean, etc.).


