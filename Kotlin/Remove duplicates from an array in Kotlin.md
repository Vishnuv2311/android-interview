Here’s your answer in README.md format:

# 🔹 Remove Duplicates from an Array in Kotlin  

## 📌 Overview  
Removing duplicates from an array in Kotlin can be done using **sets**, **distinct()**, or **filtering operations**. This ensures we get unique elements efficiently.

---

## **1️⃣ Using `toSet()` (Recommended)**
### ✅ **Converts Array to Set (Removes Duplicates Automatically)**
```kotlin
fun main() {
    val numbers = arrayOf(1, 2, 2, 3, 4, 4, 5)
    val uniqueNumbers = numbers.toSet().toTypedArray()

    println(uniqueNumbers.joinToString())  // Output: 1, 2, 3, 4, 5
}

📌 toSet() removes duplicates because a Set stores only unique values.

⸻

2️⃣ Using distinct() (Easy & Readable)

fun main() {
    val numbers = arrayOf(1, 2, 2, 3, 4, 4, 5)
    val uniqueNumbers = numbers.distinct().toTypedArray()

    println(uniqueNumbers.joinToString())  // Output: 1, 2, 3, 4, 5
}

📌 distinct() removes duplicate elements while preserving order.

⸻

3️⃣ Using filterIndexed() (Custom Filtering)

fun main() {
    val numbers = arrayOf(1, 2, 2, 3, 4, 4, 5)
    val uniqueNumbers = numbers.filterIndexed { index, value ->
        numbers.indexOf(value) == index  // Keeps only the first occurrence
    }.toTypedArray()

    println(uniqueNumbers.joinToString())  // Output: 1, 2, 3, 4, 5
}

📌 Works without converting to a Set but is less efficient than distinct().

⸻

4️⃣ Using groupBy() (For More Control)

fun main() {
    val numbers = arrayOf(1, 2, 2, 3, 4, 4, 5)
    val uniqueNumbers = numbers.groupBy { it }.keys.toTypedArray()

    println(uniqueNumbers.joinToString())  // Output: 1, 2, 3, 4, 5
}

📌 Groups elements by value and extracts unique keys.

⸻

5️⃣ Performance Comparison

Method	Preserves Order?	Time Complexity
toSet()	❌ No	O(n)
distinct()	✅ Yes	O(n)
filterIndexed()	✅ Yes	O(n²)
groupBy()	✅ Yes	O(n)



⸻

📌 Summary

✅ Use toSet() for the simplest and fastest approach (if order doesn’t matter).
✅ Use distinct() if maintaining order is required.
✅ Use filterIndexed() or groupBy() when more control is needed.


