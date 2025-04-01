# Higher-Order Functions in Kotlin

In Kotlin, a **higher-order function** is a function that takes another function as a parameter or returns a function. This allows for more flexible and concise code, enabling functional programming techniques.

## Key Features of Higher-Order Functions:
1. **Pass Functions as Arguments** – You can pass a function as a parameter to another function.
2. **Return Functions** – A function can return another function.
3. **Lambda Expressions** – They are commonly used to pass behavior as arguments.

## Example of Higher-Order Function:

```kotlin
fun operateOnNumbers(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

fun sum(x: Int, y: Int): Int = x + y

fun main() {
    val result = operateOnNumbers(5, 10, ::sum)
    println("Sum: $result") // Output: Sum: 15
}
```

## Using Lambda Expressions:
Higher-order functions often use lambdas to make the syntax more concise.

```kotlin
fun main() {
    val result = operateOnNumbers(3, 7) { x, y -> x * y }
    println("Multiplication: $result") // Output: Multiplication: 21
}
```

## Advantages of Higher-Order Functions:
- Makes code **more reusable and modular**.
- Reduces **boilerplate code**.
- Enables **functional programming** capabilities in Kotlin.

Higher-order functions are widely used in Kotlin, especially in APIs like `map`, `filter`, and `forEach`.
