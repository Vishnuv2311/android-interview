# 🔹 Extension Functions in Kotlin  

## 📌 Overview  
**Extension functions** in Kotlin allow you to **add new functionality** to existing classes **without modifying their source code**. They enable writing **clean, reusable, and more readable code** while maintaining class integrity.

---

## **1️⃣ Why Use Extension Functions?**  
✅ **Extends existing classes** without modifying their structure.  
✅ **Enhances code readability and maintainability**.  
✅ **Works with both built-in and user-defined classes**.  
✅ **Useful for utility/helper methods** to keep code DRY.  

---

## **2️⃣ How to Define an Extension Function?**  
An extension function follows this syntax:  

```kotlin
fun ClassName.functionName(): ReturnType {
    // Function body
}
```

---

## **3️⃣ Extension Function Examples**  

### **🔹 Example 1: Extending String with `reverseWords()`**
```kotlin
fun String.reverseWords(): String {
    return this.split(" ").reversed().joinToString(" ")
}

fun main() {
    val text = "Kotlin Extension Functions"
    println(text.reverseWords())  // Output: "Functions Extension Kotlin"
}
```
📌 **String class extended** without modifying its original implementation.  

---

### **🔹 Example 2: Extending `Int` with `square()`**
```kotlin
fun Int.square(): Int {
    return this * this
}

fun main() {
    println(5.square())  // Output: 25
}
```
📌 Now, `.square()` can be called like a built-in function on integers.  

---

### **🔹 Example 3: Extending Custom Class (`User`) with `isAdult()`**
```kotlin
class User(val name: String, val age: Int)

fun User.isAdult(): Boolean {
    return this.age >= 18
}

fun main() {
    val user = User("Alice", 20)
    println(user.isAdult())  // Output: true
}
```
📌 **Adds functionality** without modifying the original `User` class.  

---

## **4️⃣ Nullable Extension Functions**  

Extension functions can handle **nullable types**, preventing `NullPointerException`.

```kotlin
fun String?.safeLength(): Int {
    return this?.length ?: 0
}

fun main() {
    val name: String? = null
    println(name.safeLength())  // Output: 0
}
```
📌 Ensures safe operations on nullable values.  

---

## **5️⃣ Extension Functions vs Member Functions**  

| Feature  | Extension Function | Member Function |
|----------|-------------------|----------------|
| **Defined inside class?** | ❌ No | ✅ Yes |
| **Modifies original class?** | ❌ No | ✅ Yes |
| **Can access private members?** | ❌ No | ✅ Yes |
| **Use Case** | Utility/helper methods | Core class functionality |

---

## **📌 Summary**  

✅ **Extension functions** allow adding new methods to existing classes **without modifying their source code**.  
✅ Can be used with **built-in** and **custom classes**.  
✅ **Nullable extensions** help prevent crashes.  
✅ Do **not** modify the original class implementation, ensuring **clean and reusable code**.  
