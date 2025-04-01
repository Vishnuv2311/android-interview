# 🔹 `@JvmOverloads` Annotation in Kotlin  

## 📌 Overview  
The **`@JvmOverloads`** annotation in Kotlin is used to generate **multiple overloaded methods** for a function or constructor when calling it from Java.  

---

## **1️⃣ Why Use `@JvmOverloads`?**  
✔ **Simplifies function calls from Java** by generating default argument variations.  
✔ **Reduces the need for manual method overloading in Java**.  
✔ **Improves Java interoperability** for Kotlin functions with default parameters.  

---

## **2️⃣ How to Use `@JvmOverloads`?**
### ✅ **Without `@JvmOverloads` (Java Can't Use Default Parameters)**
```kotlin
class Example {
    fun greet(name: String = "Guest") {
        println("Hello, $name!")
    }
}

📌 Calling from Java:

Example example = new Example();
example.greet();  // ❌ ERROR: No default parameter support in Java
example.greet("Alice");  // ✅ Works

📌 Java does not support default arguments, so we must always pass parameters.

⸻

✅ With @JvmOverloads (Generates Overloaded Methods)

class Example {
    @JvmOverloads
    fun greet(name: String = "Guest", age: Int = 25) {
        println("Hello, $name! Age: $age")
    }
}

📌 Calling from Java:

example.greet();           // ✅ Works (Hello, Guest! Age: 25)
example.greet("Alice");     // ✅ Works (Hello, Alice! Age: 25)
example.greet("Alice", 30); // ✅ Works (Hello, Alice! Age: 30)

📌 Generates multiple overloaded methods, allowing Java to call without specifying all parameters.

⸻

3️⃣ @JvmOverloads with Constructors

You can also use @JvmOverloads for constructors.

class User @JvmOverloads constructor(val name: String = "Guest", val age: Int = 18)

📌 Java can now create User objects with different parameter variations.

User user1 = new User();          // ✅ Uses default values
User user2 = new User("Alice");   // ✅ Uses default age
User user3 = new User("Alice", 30); // ✅ Fully specified



⸻

4️⃣ When to Use @JvmOverloads?

Use Case	Should Use @JvmOverloads?
Functions with default parameters (called from Java)	✅ Yes
Constructors with default values	✅ Yes
Only used within Kotlin	❌ No (Unnecessary)



⸻

5️⃣ Limitations of @JvmOverloads

❌ Only applies to the last parameters in the function signature.
❌ Does not work with private functions.

@JvmOverloads
fun example(a: Int = 1, b: String) {}  // ❌ ERROR: Default parameter must be at the end



⸻

📌 Summary

✅ @JvmOverloads allows Java to use Kotlin default parameters.
✅ Generates multiple function overloads to support optional arguments.
✅ Works with constructors and functions but only for the last parameters.
✅ Not needed if calling functions only from Kotlin.


