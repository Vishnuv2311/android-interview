# 🔹 `@JvmStatic` Annotation in Kotlin  

## 📌 Overview  
The **`@JvmStatic`** annotation in Kotlin is used to **generate static methods** for Java interoperability. It allows functions inside **companion objects and objects** to be accessed as **static methods** from Java code.  

---

## **1️⃣ Why Use `@JvmStatic`?**  
✔ **Provides better Java interop** by creating actual static methods.  
✔ **Avoids extra instance calls** when accessing from Java.  
✔ **Reduces boilerplate code** for utility methods.  

---

## **2️⃣ How to Use `@JvmStatic`?**  
### ✅ **Without `@JvmStatic` (Default Behavior)**
```kotlin
class Example {
    companion object {
        fun greet() = "Hello from Kotlin"
    }
}

📌 Accessing from Java:

Example.Companion.greet();  // Requires Companion reference



⸻

✅ With @JvmStatic (Generates a True Static Method)

class Example {
    companion object {
        @JvmStatic
        fun greet() = "Hello from Kotlin"
    }
}

📌 Accessing from Java:

Example.greet();  // Direct static access (No Companion needed)



⸻

3️⃣ @JvmStatic in Objects

Since Kotlin objects are singletons, their methods are accessed via instance references in Java. Using @JvmStatic allows direct static access.

🔹 Without @JvmStatic

object Utils {
    fun log(message: String) {
        println(message)
    }
}

📌 Accessing from Java:

Utils.INSTANCE.log("Hello");  // Requires INSTANCE reference

🔹 With @JvmStatic

object Utils {
    @JvmStatic
    fun log(message: String) {
        println(message)
    }
}

📌 Accessing from Java:

Utils.log("Hello");  // Direct static call



⸻

4️⃣ When to Use @JvmStatic?

Use Case	Should Use @JvmStatic?
Access Kotlin functions from Java without Companion reference	✅ Yes
Define utility/helper methods in an object	✅ Yes
Working purely in Kotlin	❌ No (Not needed)



⸻

📌 Summary

✅ @JvmStatic generates true static methods for Java interoperability.
✅ Removes the need for .Companion or .INSTANCE references in Java.
✅ Use inside companion object or object to enable static method access.
✅ Not needed if working only in Kotlin.



