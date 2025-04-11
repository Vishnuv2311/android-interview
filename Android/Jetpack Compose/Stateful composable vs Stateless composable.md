# Stateful Composable vs Stateless Composable

Composable functions in Jetpack Compose can be categorized as **stateful** or **stateless** based on how they manage state.

## Stateless Composable
- A stateless composable does not hold or manage any state internally.
- It relies entirely on the state passed to it as parameters.
- It is reusable and easier to test.

### Example:
```kotlin
@Composable
fun StatelessCounter(counter: Int, onIncrement: () -> Unit) {
    Column {
        Text("Counter: $counter")
        Button(onClick = onIncrement) {
            Text("Increment")
        }
    }
}
```
- The `StatelessCounter` composable displays the counter value and triggers a callback when the button is clicked, but it does not manage the `counter` state itself.

## Stateful Composable
- A stateful composable manages its own state internally.
- It is responsible for updating and maintaining the state.

### Example:
```kotlin
@Composable
fun StatefulCounter() {
    var counter by remember { mutableStateOf(0) }

    Column {
        Text("Counter: $counter")
        Button(onClick = { counter++ }) {
            Text("Increment")
        }
    }
}
```
- The `StatefulCounter` composable manages the `counter` state internally using `remember`.

## Key Differences

| Feature                  | Stateless Composable               | Stateful Composable             |
|--------------------------|-------------------------------------|---------------------------------|
| **State Management**     | Relies on external state           | Manages its own state           |
| **Reusability**          | Highly reusable                    | Less reusable                   |
| **Testing**              | Easier to test                     | Harder to test due to internal state |
| **Complexity**           | Simpler                            | More complex                    |

## When to Use
- **Stateless Composable**:
  - When the state is managed externally (e.g., in a `ViewModel` or parent composable).
  - For reusable and testable components.
- **Stateful Composable**:
  - When the state is local to the composable and does not need to be shared.

## Combining Stateful and Stateless Composables
You can combine stateful and stateless composables to separate state management from UI logic.

### Example:
```kotlin
@Composable
fun CounterScreen() {
    var counter by remember { mutableStateOf(0) }

    StatelessCounter(
        counter = counter,
        onIncrement = { counter++ }
    )
}
```
- The `CounterScreen` composable manages the state, while the `StatelessCounter` composable handles the UI.

## Summary
- **Stateless composables** are reusable and rely on external state.
- **Stateful composables** manage their own state but are less reusable.
- Combining both approaches helps create modular, maintainable, and testable UIs.
