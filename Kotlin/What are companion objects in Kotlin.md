# 🛠️ Companion Objects in Kotlin  

## 📌 Overview  
A **companion object** in Kotlin is used to **define static members** inside a class. It allows functions and properties to be accessed **without creating an instance** of the class.  

---

## **1️⃣ Why Use Companion Objects?**  
✔ **Replaces static methods from Java**.  
✔ **Allows access to class members without instantiation**.  
✔ **Can implement interfaces** like normal objects.  
✔ **Supports dependency injection in classes**.  

---

## **2️⃣ How to Define a Companion Object?**  
```kotlin
class MyClass {
    companion object {
        val constantValue = 100

        fun printMessage() {
            println("Hello from Companion Object!")
        }
    }
}

fun main() {
    println(MyClass.constantValue)  // ✅ Access without instance
    MyClass.printMessage()  // ✅ Access function without instance
}

✅ Output:

100  
Hello from Companion Object!

📌 The companion object acts like a static member in Java.

⸻

3️⃣ Using Companion Objects with a Factory Pattern

Companion objects are useful for creating instances of a class (Factory Pattern).

class User private constructor(val name: String) {
    companion object {
        fun create(name: String): User {
            return User(name)
        }
    }
}

fun main() {
    val user = User.create("Alice")  // ✅ Create User without constructor
    println(user.name)
}

📌 Useful when you need a controlled way to create objects.

⸻

4️⃣ Implementing Interfaces in Companion Objects

Companion objects can implement interfaces, making them more powerful.

interface Logger {
    fun log(message: String)
}

class MyClass {
    companion object : Logger {
        override fun log(message: String) {
            println("Log: $message")
        }
    }
}

fun main() {
    MyClass.log("Companion Objects are powerful!")
}

✅ Output:

Log: Companion Objects are powerful!

📌 Allows defining behaviors inside companion objects.

⸻

5️⃣ Companion Objects vs object Keyword

Feature	Companion Object	object Declaration
Access Type	Inside a class	Standalone object
Requires Class Instance?	❌ No	❌ No
Implements Interfaces?	✅ Yes	✅ Yes
Similar to Java static?	✅ Yes	❌ No



⸻

📌 Summary

✅ Companion objects allow defining static-like functions and properties.
✅ Used for factory methods, constants, and singleton patterns.
✅ Can implement interfaces like a normal object.
✅ No need to instantiate the class to access companion object members.


