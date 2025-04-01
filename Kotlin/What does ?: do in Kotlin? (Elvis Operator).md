# What does ?: do in Kotlin? (Elvis Operator)

The `?:` operator in Kotlin is called the **Elvis operator**. It is used to provide a default value when an expression evaluates to `null`. It is commonly used for handling nullable variables efficiently.

## Syntax:
```kotlin
val result = nullableValue ?: defaultValue
```
If `nullableValue` is not `null`, `result` will be assigned its value. Otherwise, `result` will take the `defaultValue`.

## Example Usage:
```kotlin
val name: String? = null
val displayName: String = name ?: "Guest"

println(displayName) // Output: Guest
```

## Use Case:
- Helps to provide default values for nullable variables.
- Makes null-checking more concise and readable.
- Avoids explicit `if-else` null checks.

## Example with Function:
```kotlin
fun getLength(str: String?): Int {
    return str?.length ?: 0
}

println(getLength("Hello")) // Output: 5
println(getLength(null))    // Output: 0
```

The Elvis operator is a powerful feature in Kotlin that simplifies null safety handling and improves code readability.
