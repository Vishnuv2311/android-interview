# What is State Hoisting in Jetpack Compose?

State hoisting is a design pattern in Jetpack Compose where state is moved to a composable's caller to make it easier to manage and share.

## Purpose of State Hoisting
- To separate state management from UI logic.
- To make composables more reusable and testable.
- To allow the parent composable to control the state.

## Benefits of State Hoisting
1. **Single Source of Truth**:
   - The state is managed in one place, reducing inconsistencies.
2. **Reusability**:
   - Composables become stateless and can be reused in different contexts.
3. **Testability**:
   - Stateless composables are easier to test.

## How State Hoisting Works
A composable exposes:
1. The current state as a parameter.
2. Events (e.g., callbacks) to request state changes.

## Example
### Stateless Composable
```kotlin
@Composable
fun Counter(value: Int, onValueChange: (Int) -> Unit) {
    Button(onClick = { onValueChange(value + 1) }) {
        Text("Counter: $value")
    }
}
```

### Stateful Composable
```kotlin
@Composable
fun CounterScreen() {
    var counter by remember { mutableStateOf(0) }

    Counter(value = counter, onValueChange = { counter = it })
}
```
- `Counter` is a stateless composable that takes `value` and `onValueChange` as parameters.
- `CounterScreen` manages the state and passes it to `Counter`.

## Best Practices
- Hoist state when a composable needs to be reusable or when the state needs to be shared.
- Avoid hoisting state unnecessarily, as it can make the code harder to follow.

## Summary
State hoisting in Jetpack Compose is a pattern that separates state management from UI logic, making composables more reusable, testable, and easier to manage.
