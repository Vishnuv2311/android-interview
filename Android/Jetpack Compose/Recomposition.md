# Recomposition in Jetpack Compose

Recomposition is a key concept in Jetpack Compose that ensures the UI is updated when the state changes.

## What is Recomposition?
- Recomposition is the process of re-executing composable functions to update the UI when the state they depend on changes.
- It is efficient and only updates the parts of the UI that need to change.

## How Recomposition Works
1. A composable function is executed for the first time to build the UI.
2. When the state used by the composable changes, the function is re-executed.
3. Compose intelligently skips recomposing parts of the UI that haven't changed.

## Example:
```kotlin
@Composable
fun RecompositionExample() {
    var counter by remember { mutableStateOf(0) }

    Column {
        Button(onClick = { counter++ }) {
            Text("Increment")
        }
        Text("Counter: $counter")
    }
}
```
- In this example, only the `Text` composable displaying the counter value is recomposed when `counter` changes.

## Key Points
- Recomposition is triggered by changes in `State` or `MutableState`.
- Compose optimizes recomposition by skipping unchanged parts of the UI.
- Avoid unnecessary recompositions by keeping state localized to the composable that needs it.

## Best Practices
- Use `remember` or `rememberSaveable` to manage state efficiently.
- Minimize the scope of recomposition by structuring your composables properly.
