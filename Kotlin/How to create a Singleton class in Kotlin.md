# How to create a Singleton class in Kotlin

In Kotlin, you can create a Singleton class using the `object` keyword. Unlike Java, where you need to manage a private constructor and a static instance, Kotlin provides a straightforward way to define a Singleton.

## Example:
```kotlin
object Singleton {
    fun doSomething() {
        println("Singleton function called")
    }
}

fun main() {
    Singleton.doSomething()
}
```

## Explanation:
- The `object` declaration creates a Singleton instance.
- It is thread-safe and lazy-initialized automatically.
- There is no need for manual instantiation.

## Alternative: Singleton with Companion Object
If you need a Singleton inside a class but still require an instance of the class:
```kotlin
class SingletonWithCompanion private constructor() {
    companion object {
        @Volatile
        private var INSTANCE: SingletonWithCompanion? = null

        fun getInstance(): SingletonWithCompanion {
            return INSTANCE ?: synchronized(this) {
                INSTANCE ?: SingletonWithCompanion().also { INSTANCE = it }
            }
        }
    }
}
```
- This approach follows the classic Singleton pattern with lazy initialization and thread safety.
