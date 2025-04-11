# `remember` vs `rememberSaveable` in Jetpack Compose

Both `remember` and `rememberSaveable` are used to manage state in Jetpack Compose, but they serve different purposes.

## `remember`
- Retains state across recompositions.
- Does **not** survive configuration changes (e.g., screen rotations).
- Use it for transient state that doesn't need to persist.

### Example:
```kotlin
@Composable
fun RememberExample() {
    var counter by remember { mutableStateOf(0) }

    Button(onClick = { counter++ }) {
        Text("Counter: $counter")
    }
}
```
- The `counter` value resets to `0` after a configuration change.

## `rememberSaveable`
- Retains state across recompositions **and** survives configuration changes.
- Uses `SavedStateHandle` or `Bundle` under the hood to persist state.
- Use it for state that needs to persist across configuration changes.

### Example:
```kotlin
@Composable
fun RememberSaveableExample() {
    var counter by rememberSaveable { mutableStateOf(0) }

    Button(onClick = { counter++ }) {
        Text("Counter: $counter")
    }
}
```
- The `counter` value persists even after a configuration change.

## Key Differences

| Feature                  | `remember`                  | `rememberSaveable`           |
|--------------------------|-----------------------------|------------------------------|
| Survives recomposition   | Yes                         | Yes                          |
| Survives configuration changes | No                          | Yes                          |
| Use case                 | Transient state             | Persistent state             |

## When to Use
- Use `remember` for temporary state that doesn't need to survive configuration changes (e.g., animations, UI-only state).
- Use `rememberSaveable` for state that should persist across configuration changes (e.g., form inputs, counters).

## Summary
- `remember` is lightweight and suitable for transient state.
- `rememberSaveable` is more robust and should be used when state persistence is required.
