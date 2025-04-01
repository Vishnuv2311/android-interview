# What are Lambdas in Kotlin?

In Kotlin, a **lambda expression** is a concise way to define an anonymous function. It is a function that can be passed as an argument or stored in a variable.

## Syntax of a Lambda
```kotlin
val sum: (Int, Int) -> Int = { a, b -> a + b }
println(sum(5, 3)) // Output: 8
```

### Characteristics of Lambda Expressions:
1. **No need for a function name**: Unlike regular functions, lambdas don’t require explicit names.
2. **Can be assigned to variables**: A lambda expression can be stored in a variable and invoked like a regular function.
3. **Can be passed as arguments**: Lambdas are often used as function parameters, making them useful for higher-order functions.

## Example: Using Lambda in a Higher-Order Function
```kotlin
fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

val result = calculate(10, 5) { x, y -> x - y }
println(result) // Output: 5
```

## Implicit `it` Parameter
If a lambda has only one parameter, we can use `it` instead of explicitly defining the parameter.
```kotlin
val square: (Int) -> Int = { it * it }
println(square(4)) // Output: 16
```

## Conclusion
Lambdas in Kotlin provide a concise way to define functions, making the code more readable and expressive. They are widely used in functional programming and are essential for writing clean Kotlin code.
