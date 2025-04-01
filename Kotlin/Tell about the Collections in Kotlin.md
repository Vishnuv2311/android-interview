# Collections in Kotlin

Kotlin provides a powerful and flexible collection framework to store, manipulate, and process data efficiently. Collections in Kotlin can be categorized into two types:

## 1. Immutable Collections
Immutable collections cannot be modified after they are created. Kotlin provides built-in immutable collection types:
- `List<T>`: Ordered collection of elements (e.g., `listOf(1, 2, 3)`)
- `Set<T>`: Unordered collection of unique elements (e.g., `setOf("a", "b", "c")`)
- `Map<K, V>`: Key-value pairs, where keys are unique (e.g., `mapOf("key1" to "value1")`)

## 2. Mutable Collections
Mutable collections allow modifications such as adding, removing, or updating elements. Kotlin provides mutable versions of collections:
- `MutableList<T>`: Allows modifications (e.g., `mutableListOf(1, 2, 3)`)
- `MutableSet<T>`: Allows adding and removing unique elements (e.g., `mutableSetOf("x", "y", "z")`)
- `MutableMap<K, V>`: Allows modification of key-value pairs (e.g., `mutableMapOf("a" to 1, "b" to 2)`)

## 3. Important Collection Functions
Kotlin provides various extension functions to work with collections:
- `filter {}`: Filters elements based on a condition.
- `map {}`: Transforms each element.
- `forEach {}`: Iterates over each element.
- `reduce {}` / `fold {}`: Accumulates values.
- `groupBy {}`: Groups elements based on a key.
- `sortedBy {}`: Sorts elements based on a given selector.

## 4. Collection Builders
Kotlin offers `buildList {}` and `buildSet {}` to construct collections dynamically.

### Example:
```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers) // Output: [2, 4]
```

Kotlin collections are designed to be concise, efficient, and expressive, making them a powerful tool for handling data structures in Android and general development.
