# What are Labels in Kotlin?

In Kotlin, **labels** are identifiers that allow us to name loops and expressions, making it easier to control the flow of execution. They are primarily used with `break`, `continue`, and `return` statements to specify which loop or function they should apply to.

## Syntax
A label is defined by prefixing an identifier with `@`. Example:
```kotlin
labelName@ for (i in 1..5) {
    for (j in 1..5) {
        if (i == 3 && j == 3) break@labelName  // Breaks out of both loops
        println("i = $i, j = $j")
    }
}
```

## Use Cases
1. **Breaking Out of Nested Loops**  
   Using labels, you can break out of multiple nested loops.
   ```kotlin
   outer@ for (i in 1..3) {
       for (j in 1..3) {
           if (i == 2 && j == 2) break@outer
           println("i = $i, j = $j")
       }
   }
   ```

2. **Skipping Iterations with `continue`**
   ```kotlin
   outer@ for (i in 1..3) {
       for (j in 1..3) {
           if (j == 2) continue@outer  // Skips remaining iterations for 'i'
           println("i = $i, j = $j")
       }
   }
   ```

3. **Returning from a Lambda**
   ```kotlin
   fun example() {
       listOf(1, 2, 3, 4, 5).forEach label@{
           if (it == 3) return@label  // Exits only the lambda, not the function
           println(it)
       }
       println("End of function")  // This will be printed
   }
   ```

## Conclusion
Labels in Kotlin provide a flexible way to control loops and function execution. They help improve code readability by making the flow of execution explicit.
