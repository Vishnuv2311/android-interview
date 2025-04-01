# Difference between `==` and `===` in Kotlin

In Kotlin, `==` and `===` are used for comparisons, but they serve different purposes:

## `==` (Structural Equality)
- Checks if two objects have the same content.
- Internally calls the `equals()` method.
- Example:
  ```kotlin
  val a = "Hello"
  val b = "Hello"
  println(a == b) // true (content is the same)
  ```

## `===` (Referential Equality)
- Checks if two objects refer to the same memory location.
- Does not compare content, only references.
- Example:
  ```kotlin
  val a = "Hello"
  val b = "Hello"
  println(a === b) // false (different memory references in some cases)
  val c = a
  println(a === c) // true (same reference)
  ```

