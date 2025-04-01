# How to Choose Between `apply` and `with` in Kotlin

## `apply`
- Used when configuring an object.
- Returns the same object it was called on.
- Typically used when initializing objects.

### Example:
```kotlin
val person = Person().apply {
    name = "John"
    age = 30
}
```

## `with`
- Used when performing operations on an object.
- Returns the last expression value inside its block.
- Useful when calling multiple methods on an object.

### Example:
```kotlin
val result = with(person) {
    name = "Doe"
    age = 25
    "Updated successfully"
}
```

### When to Use Which?
- Use `apply` when configuring an object.
- Use `with` when performing actions and retrieving a result.
