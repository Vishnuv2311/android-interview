# What is an init block in Kotlin?

An **`init` block** in Kotlin is a special block inside a class that executes when an instance of the class is created. It is mainly used for initialization purposes.

## Key Features:
- The **`init` block** runs **before** any secondary constructors.
- It is used to **initialize** properties or perform **setup operations**.
- Multiple **`init` blocks** can be defined in a class, and they execute in order.

## Example:
```kotlin
class Person(val name: String, val age: Int) {
    init {
        println("Person object is being created: Name = $name, Age = $age")
    }
}

fun main() {
    val person = Person("John", 25)
}
```
**Output:**
```
Person object is being created: Name = John, Age = 25
```

## Multiple `init` Blocks Example
```kotlin
class Example(val number: Int) {
    init {
        println("First init block: Number is $number")
    }

    init {
        println("Second init block: Square of number is ${number * number}")
    }
}

fun main() {
    val example = Example(5)
}
```
**Output:**
```
First init block: Number is 5
Second init block: Square of number is 25
```

## Why Use an `init` Block?
- To **validate constructor parameters** before using them.
- To **execute logic when an instance is created**.
- To **initialize non-lazy properties**.
