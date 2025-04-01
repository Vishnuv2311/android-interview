# 📄 Data Class in Kotlin  

## 📌 Overview  
A **data class** in Kotlin is a special class used to **store data**. It automatically provides useful functions like:  
✔ `toString()` – Converts object to readable string.  
✔ `equals()` – Compares objects by their values.  
✔ `hashCode()` – Generates unique hash for each object.  
✔ `copy()` – Creates a new object with modified values.  

---

## **1️⃣ How to Define a Data Class?**  
A data class is declared using the **`data`** keyword.  

```kotlin
data class User(val name: String, val age: Int)

✅ Example: Using a Data Class

fun main() {
    val user1 = User("Alice", 25)
    val user2 = User("Alice", 25)

    println(user1)  // Output: User(name=Alice, age=25)
    println(user1 == user2)  // Output: true (compares values, not references)
}

📌 Data classes automatically generate toString() and equals() methods.

⸻

2️⃣ Key Features of Data Classes

Feature	Description
Auto-generated toString()	Prints object properties
equals() & hashCode()	Compares values, useful in collections
copy() method	Creates a new object with modified values
Component functions	Supports destructuring (val (name, age) = user)



⸻

3️⃣ Using copy() to Modify Data

fun main() {
    val user1 = User("Alice", 25)
    val user2 = user1.copy(age = 30)

    println(user2)  // Output: User(name=Alice, age=30)
}

📌 Creates a new object while keeping some properties unchanged.

⸻

4️⃣ Destructuring a Data Class

Data classes support destructuring declarations, allowing you to extract values easily.

fun main() {
    val user = User("Alice", 25)
    val (name, age) = user  // Destructuring

    println("Name: $name, Age: $age")  // Output: Name: Alice, Age: 25
}

📌 Useful for simplifying variable assignments.

⸻

5️⃣ Data Class vs Regular Class

Feature	Data Class	Regular Class
Auto-generated functions (toString(), equals(), etc.)	✅ Yes	❌ No
Primary Constructor Required	✅ Yes	❌ No
Ideal for storing data	✅ Yes	❌ No
Use case	Immutable data objects	Business logic



⸻

6️⃣ Rules for Creating a Data Class

✔ Must have at least one property in the primary constructor.
✔ Properties should be val or var (immutable is preferred).
✔ Cannot be abstract, sealed, open, or inner.

⸻

📌 Summary

✅ Data classes store and manage data efficiently.
✅ Auto-generate useful methods (toString(), equals(), copy()).
✅ Best for modeling immutable data (e.g., API responses, database entities).
✅ Supports destructuring for easy data extraction.

