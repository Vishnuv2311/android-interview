# Difference between `val` and `var` in Kotlin

In Kotlin, `val` and `var` are used to declare variables, but they have different properties:

## `val` (Immutable)
- Stands for **value**.
- Declares a **read-only** variable (immutable).
- Once assigned, the value cannot be changed.
- Similar to `final` in Java.

**Example:**
```kotlin
val name = "Kotlin"
name = "Java" // Compilation error
```

## `var` (Mutable)
- Stands for **variable**.
- Declares a **mutable** variable.
- The value can be reassigned.

**Example:**
```kotlin
var age = 25
age = 30 // No error, value is updated
```

## Key Differences
| Feature   | `val` | `var` |
|-----------|------|------|
| Mutability | Immutable | Mutable |
| Reassignment | Not allowed | Allowed |
| Similar to | `final` in Java | Regular variable |

Use `val` when you don’t need to change the value, and `var` when the value needs to be updated.
