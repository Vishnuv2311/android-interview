# Visibility Modifiers in Kotlin

Kotlin provides four visibility modifiers to control the accessibility of classes, objects, interfaces, constructors, functions, and properties.

## 1. **public (default)**
- Accessible from anywhere.
- If no modifier is specified, `public` is used by default.
- Example:
  ```kotlin
  class PublicClass {
      fun publicFunction() {
          println("This is a public function")
      }
  }
  ```

## 2. **private**
- Accessible only within the same file or enclosing class.
- Useful for encapsulation.
- Example:
  ```kotlin
  class PrivateExample {
      private val secret = "Hidden"

      private fun privateFunction() {
          println(secret)
      }
  }
  ```

## 3. **protected**
- Similar to `private` but also accessible in subclasses.
- Not applicable to top-level declarations (only within classes).
- Example:
  ```kotlin
  open class Parent {
      protected fun protectedFunction() {
          println("Protected function")
      }
  }

  class Child : Parent() {
      fun accessProtected() {
          protectedFunction() // Allowed
      }
  }
  ```

## 4. **internal**
- Accessible within the same module.
- Useful for hiding implementation details from external modules.
- Example:
  ```kotlin
  internal class InternalClass {
      internal fun internalFunction() {
          println("This is an internal function")
      }
  }
  ```

## Summary Table

| Modifier  | Accessible Within            | Top-Level Allowed? |
|-----------|-----------------------------|-------------------|
| `public`  | Everywhere                    | Yes |
| `private` | Same file or enclosing class   | Yes (file-private) |
| `protected` | Same class & subclasses     | No |
| `internal` | Same module                   | Yes |
