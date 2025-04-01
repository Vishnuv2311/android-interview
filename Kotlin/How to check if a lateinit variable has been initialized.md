# How to check if a lateinit variable has been initialized in Kotlin

In Kotlin, `lateinit` is used to declare a variable that will be initialized later. However, accessing an uninitialized `lateinit` variable will throw an `UninitializedPropertyAccessException`. To check if a `lateinit` variable has been initialized before accessing it, use the `::propertyName.isInitialized` syntax.

## Example:

```kotlin
class Example {
    lateinit var name: String

    fun checkInitialization() {
        if (::name.isInitialized) {
            println("The variable 'name' has been initialized.")
        } else {
            println("The variable 'name' has NOT been initialized.")
        }
    }
}

fun main() {
    val example = Example()
    example.checkInitialization() // Output: The variable 'name' has NOT been initialized.
    
    example.name = "Kotlin"
    example.checkInitialization() // Output: The variable 'name' has been initialized.
}
```

## Notes:
- The `::propertyName.isInitialized` check works only for `lateinit var` properties inside a class.
- It does not work with `lateinit var` declared at the top level or inside an object.
- Using `lateinit` is beneficial when dependency injection or initialization at a later stage is required.
