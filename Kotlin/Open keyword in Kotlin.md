# Open Keyword in Kotlin

In Kotlin, the `open` keyword is used to allow classes and member functions to be inherited or overridden. By default, all classes and functions in Kotlin are `final`, meaning they cannot be extended or overridden.

## Usage

- **Open Class**: A class must be marked with `open` if you want to allow it to be subclassed.
- **Open Function**: A function inside a class must be marked with `open` if it should be overridden in derived classes.

## Example

```kotlin
open class Animal {
    open fun makeSound() {
        println("Animal makes a sound")
    }
}

class Dog : Animal() {
    override fun makeSound() {
        println("Dog barks")
    }
}

fun main() {
    val dog = Dog()
    dog.makeSound() // Output: Dog barks
}
```

## Key Points
- If a class is not marked as `open`, it cannot be inherited.
- If a function is not marked as `open`, it cannot be overridden.
- This behavior enforces better encapsulation and immutability by default.
