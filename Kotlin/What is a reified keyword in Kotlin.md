

# 🔹 `reified` Keyword in Kotlin
 
 ## 📌 Overview  
 The **`reified`** keyword in Kotlin is used with **inline functions** to retain **generic type information** at runtime. Normally, type parameters in generics are erased at runtime (type erasure), but `reified` prevents this.
 
 ---
 
 ## **1️⃣ Why Use `reified`?**  
 ✔ **Allows access to generic type information at runtime**.  
 ✔ **Removes the need for `Class<T>` parameters**.  
 ✔ **Simplifies reflection-based operations**.  
 
 ---
 
 ## **2️⃣ Problem Without `reified` (Type Erasure)**
 ```kotlin
 fun <T> getType(): String {
     return T::class.simpleName  // ❌ ERROR: Type information is erased
 }
 ```
 📌 **Generics in Kotlin are erased at runtime, so this won't work.**  
 
 ---
 
 ## **3️⃣ Using `reified` to Retain Type Information**
 ```kotlin
 inline fun <reified T> getType(): String {
     return T::class.simpleName ?: "Unknown"
 }
 
 fun main() {
     println(getType<String>())  // Output: String
     println(getType<Int>())     // Output: Int
 }
 ```
 📌 **The `reified` keyword allows access to `T::class` at runtime.**  
 
 ---
 
 ## **4️⃣ Example: Filtering a List Using `reified`**
 ```kotlin
 inline fun <reified T> List<Any>.filterByType(): List<T> {
     return this.filterIsInstance<T>()
 }
 
 fun main() {
     val items = listOf(1, "Kotlin", 2.5, "Hello", 42)
     val strings = items.filterByType<String>()
     println(strings)  // Output: [Kotlin, Hello]
 }
 ```
 📌 **Filters elements of a list based on a specific type.**  
 
 ---
 
 ## **5️⃣ When to Use `reified`?**
 | Use Case | Should Use `reified`? |
 |----------|------------------|
 | **Retrieve class type of a generic parameter** | ✅ Yes |
 | **Reflection-based operations (`T::class`)** | ✅ Yes |
 | **Filtering elements by type (`filterIsInstance<T>()`)** | ✅ Yes |
 | **Pass generic type to another function** | ❌ No |
 
 ---
 
 ## **📌 Summary**
 ✅ **`reified` allows access to generic type information at runtime.**  
 ✅ **Useful in inline functions where type information is needed.**  
 ✅ **Avoids passing `Class<T>` explicitly for type operations.**  
 ✅ **Best for filtering, logging, and reflection-based functions.**  
 