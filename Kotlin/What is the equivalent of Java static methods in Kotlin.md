# What is the Equivalent of Java Static Methods in Kotlin?

In Java, static methods belong to a class rather than to instances of the class. Kotlin does not have a direct `static` keyword, but there are several ways to achieve similar functionality:

## 1. Using Companion Object
```kotlin
class Example {
    companion object {
        fun staticMethod() {
            println("This is a static-like method in Kotlin")
        }
    }
}

fun main() {
    Example.staticMethod()
}
```

- The `companion object` allows us to define methods that behave similarly to static methods in Java.
  
## 2. Using Top-Level Functions
```kotlin
fun staticMethod() {
    println("This is a top-level function in Kotlin")
}

fun main() {
    staticMethod()
}
```

- Kotlin allows defining functions at the top level of a file, making them accessible without needing an instance of a class.

## 3. Using Object Declaration (Singleton)
```kotlin
object SingletonExample {
    fun staticMethod() {
        println("This is a static-like method using an object declaration")
    }
}

fun main() {
    SingletonExample.staticMethod()
}
```

- The `object` keyword creates a singleton, which can have methods similar to static methods in Java.

## 4. Using @JvmStatic Annotation
```kotlin
class Example {
    companion object {
        @JvmStatic
        fun staticMethod() {
            println("This is a static method with @JvmStatic annotation")
        }
    }
}

fun main() {
    Example.staticMethod()
}
```

- The `@JvmStatic` annotation allows calling the method as a static method when accessed from Java.

## Conclusion
Kotlin provides multiple ways to mimic Java's static methods, including `companion objects`, top-level functions, singletons, and the `@JvmStatic` annotation.
