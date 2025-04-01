# Difference Between `open` and `public` in Kotlin

In Kotlin, `open` and `public` serve different purposes when defining classes and functions.

## `public`
- `public` is the default visibility modifier in Kotlin.
- It means that a class, function, or property is accessible from anywhere.
- Example:
  ```kotlin
  class PublicClass {
      public fun greet() {
          println("Hello!")
      }
  }
  ```

## `open`
- By default, classes and methods in Kotlin are `final`, meaning they cannot be inherited or overridden.
- The `open` keyword is used to allow inheritance and overriding.
- Example:
  ```kotlin
  open class OpenClass {
      open fun greet() {
          println("Hello from OpenClass!")
      }
  }
  
  class DerivedClass : OpenClass() {
      override fun greet() {
          println("Hello from DerivedClass!")
      }
  }
  ```

## Key Differences
| Feature   | `public` | `open` |
|-----------|---------|--------|
| Purpose   | Defines visibility (who can access it) | Allows inheritance/overriding |
| Default   | Everything is `public` by default | Classes and functions are `final` by default |
| Effect on Inheritance | No impact | Must be explicitly used for inheritance |

### Summary
- `public` controls access but does not affect inheritance.
- `open` allows classes and methods to be inherited and overridden.
