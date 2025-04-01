# Advantage of using `const` in Kotlin

In Kotlin, the `const` keyword is used to declare compile-time constants. These constants offer several advantages:

## Advantages of `const`:
  
1. **Performance Optimization**: Since `const` values are resolved at compile time, they eliminate runtime calculations, making the code more efficient.
2. **Memory Efficiency**: `const` values are stored in the compiled bytecode rather than being instantiated at runtime, reducing memory usage.
3. **Immutable by Default**: `const` values are immutable, ensuring data integrity and reducing potential bugs caused by accidental modification.
4. **Global Access**: `const` properties are usually declared at the top level or inside `companion objects`, making them accessible across the application.
5. **Use in Annotations**: `const` values can be used in annotations, whereas normal `val` properties cannot.

## Example:

```kotlin
object Constants {
    const val API_URL = "https://api.example.com"
    const val TIMEOUT = 5000
}

fun main() {
    println(Constants.API_URL) // Output: https://api.example.com
    println(Constants.TIMEOUT) // Output: 5000
}
```

## When to Use `const`?
- When you need a value that does not change and is known at compile time.
- When defining constant values that will be reused across multiple files.
- When you want to avoid unnecessary memory allocation at runtime.

## Limitations of `const`
- `const` can only be used with **primitive types (Int, String, Boolean, etc.)** and **String literals**.
- It cannot be used with non-primitive types such as lists or objects.
- `const` must be declared at the **top level** or inside a `companion object`.

Using `const` ensures better performance and readability in Kotlin programs.
