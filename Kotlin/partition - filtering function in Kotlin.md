# partition - Filtering Function in Kotlin

The `partition` function in Kotlin is used to split a collection into two lists based on a given predicate. It returns a `Pair` of lists, where the first list contains elements that satisfy the predicate, and the second list contains elements that do not.

## Syntax
```kotlin
val (matching, nonMatching) = list.partition { condition }
```

## Example Usage
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

    // Partition the list into even and odd numbers
    val (evenNumbers, oddNumbers) = numbers.partition { it % 2 == 0 }

    println("Even numbers: $evenNumbers")
    println("Odd numbers: $oddNumbers")
}
```

### Output
```
Even numbers: [2, 4, 6, 8, 10]
Odd numbers: [1, 3, 5, 7, 9]
```

## Use Cases
- Filtering data into two groups based on a condition.
- Separating valid and invalid entries in a list.
- Useful in scenarios where you need to process two subsets differently.
