# 🔹 Advantages of Using `const` in Kotlin  

## 📌 Overview  
In Kotlin, `const` is used to declare **compile-time constants**. It is used with `val` and must be **initialized with a primitive or String** at the time of declaration.

---

## **1️⃣ Why Use `const`?**  
| Feature | Benefit |
|---------|---------|
| **Compile-time constant** | Value is **determined at compile time**, improving performance. |
| **Faster than `val`** | No memory allocation at runtime. |
| **Cannot be changed** | Ensures **immutability and safety**. |
| **Stored in bytecode** | Reduces **runtime overhead** by storing values in class metadata. |

---

## **2️⃣ How to Use `const`?**  
### ✅ **Declaration Syntax**
```kotlin
const val MAX_USERS = 100
const val APP_NAME = "KotlinApp"

📌 Must be inside a top-level object or companion object.

⸻

3️⃣ const vs val

Feature	const	val
Assigned at	Compile-time	Runtime
Allowed Data Types	Primitives, Strings	Any type
Used in functions?	❌ No	✅ Yes
Stored in memory?	Directly in bytecode	Allocated at runtime

🔹 Example of const vs val

const val CONST_VALUE = "Compile-time"  // ✅ Works

val runtimeValue = System.currentTimeMillis()  // ❌ Cannot be `const`

📌 const values must be known at compile time.

⸻

4️⃣ Where to Use const?

Use Case	Should Use const?
Static API keys, App names	✅ Yes
Configuration values (e.g., timeouts)	✅ Yes
Function return values	❌ No
Changing variables at runtime	❌ No



⸻

📌 Summary

✅ Use const for compile-time constants (improves performance).
✅ Must be used with val inside top-level or companion objects.
✅ Faster than val since no runtime allocation.
✅ Only works with primitives and Strings.


