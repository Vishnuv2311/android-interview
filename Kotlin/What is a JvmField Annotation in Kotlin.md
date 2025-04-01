Here’s your answer in README.md format:

# 🔹 `@JvmField` Annotation in Kotlin  

## 📌 Overview  
The **`@JvmField`** annotation in Kotlin is used to expose **Kotlin properties as public fields** in Java, removing the need for getters and setters.  

---

## **1️⃣ Why Use `@JvmField`?**  
✔ **Removes generated getter methods** when accessing properties from Java.  
✔ **Provides direct field access**, improving Java interoperability.  
✔ **Reduces boilerplate code** by eliminating accessor methods.  

---

## **2️⃣ How to Use `@JvmField`?**  
### ✅ **Without `@JvmField` (Default Behavior)**
```kotlin
class Example {
    val name: String = "Kotlin"
}

📌 Accessing from Java:

Example example = new Example();
String value = example.getName();  // Uses getter method



⸻

✅ With @JvmField (Removes Getter)

class Example {
    @JvmField
    val name: String = "Kotlin"
}

📌 Accessing from Java:

Example example = new Example();
String value = example.name;  // Direct field access (No getter)



⸻

3️⃣ Using @JvmField in a companion object

By default, companion object properties require .Companion reference in Java. @JvmField removes this requirement.

class Example {
    companion object {
        @JvmField
        val constant = "Hello"
    }
}

📌 Accessing from Java:

String value = Example.constant;  // No need for Example.Companion.constant



⸻

4️⃣ When to Use @JvmField?

Use Case	Should Use @JvmField?
Expose a property as a public field to Java	✅ Yes
Reduce unnecessary getter methods	✅ Yes
Use in a companion object for static fields	✅ Yes
Private fields or custom getters	❌ No



⸻

5️⃣ @JvmField vs @JvmStatic

Feature	@JvmField	@JvmStatic
Applied To	Properties (val / var)	Functions (fun)
Removes Getters?	✅ Yes	❌ No
Removes Companion Reference in Java?	✅ Yes	✅ Yes



⸻

📌 Summary

✅ @JvmField exposes Kotlin properties as public fields in Java.
✅ Removes unnecessary getter methods for better Java interop.
✅ Useful in companion object to access constants without .Companion reference.
✅ Not needed if working purely in Kotlin.

