# Companion Object in Kotlin

In Kotlin, a **companion object** is an object that is tied to a class rather than to instances of the class. It allows us to define static-like methods and properties inside a class.

## Syntax:
```kotlin
class MyClass {
    companion object {
        fun myStaticMethod() {
            println("Hello from companion object!")
        }
    }
}

fun main() {
    MyClass.myStaticMethod() // No need to create an instance
}
```

## Key Points:
- A **companion object** is declared inside a class using the `companion` keyword.
- It behaves similarly to static methods in Java.
- We can access its members using the class name.
- A class can have only **one** companion object.

## Example with Properties:
```kotlin
class Counter {
    companion object {
        var count = 0

        fun increment() {
            count++
        }
    }
}

fun main() {
    println(Counter.count) // 0
    Counter.increment()
    println(Counter.count) // 1
}
```

## Naming a Companion Object:
By default, a companion object does not require a name, but we can explicitly name it:
```kotlin
class Example {
    companion object NamedObject {
        fun showMessage() = println("Named companion object")
    }
}

fun main() {
    Example.showMessage() // Named companion object
}
```

## Conclusion:
Companion objects provide a convenient way to define **static-like** members in Kotlin classes while maintaining the benefits of object-oriented design.
