# Higher-Order Function that Returns a Function in Kotlin

A higher-order function is a function that takes another function as a parameter or returns a function. Below is an example of a Kotlin function that returns another function:

```kotlin
fun operation(operator: String): (Int, Int) -> Int {
    return when (operator) {
        "add" -> { a, b -> a + b }
        "subtract" -> { a, b -> a - b }
        "multiply" -> { a, b -> a * b }
        "divide" -> { a, b -> if (b != 0) a / b else throw ArithmeticException("Cannot divide by zero") }
        else -> throw IllegalArgumentException("Unknown operator")
    }
}

fun main() {
    val addFunction = operation("add")
    println(addFunction(5, 3)) // Output: 8

    val multiplyFunction = operation("multiply")
    println(multiplyFunction(4, 2)) // Output: 8
}

## Explanation:
- The `operation` function takes a `String` as a parameter (operator).
- It returns a lambda function that takes two integers and performs the operation specified.
- The returned function can then be called with two integer arguments.

This approach allows us to dynamically return different functions based on the provided argument.
