# State in Jetpack Compose: `remember`, `rememberSaveable`, and `MutableState`

In Jetpack Compose, managing state is crucial for building dynamic and interactive UIs. Below are the key concepts:

## `remember`
- `remember` is used to store a value in memory during recompositions.
- It helps retain state across recompositions but does not survive configuration changes like screen rotations.

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

## `rememberSaveable`
- `rememberSaveable` works like `remember` but also saves the state during configuration changes (e.g., screen rotations).
- It uses `Bundle` under the hood to persist the state.

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

## `MutableState`
- `MutableState` is a type that holds a value and notifies observers when the value changes.
- It is commonly used with `remember` or `rememberSaveable` to create reactive state.

### Example:
```kotlin
@Composable
fun MutableStateExample() {
    val textState = remember { mutableStateOf("Hello") }

    Column {
        TextField(
            value = textState.value,
            onValueChange = { textState.value = it }
        )
        Text("You typed: ${textState.value}")
    }
}
```

## Summary
- Use `remember` for transient state that doesn't need to survive configuration changes.
- Use `rememberSaveable` for state that should persist across configuration changes.
- Use `MutableState` to create reactive state that updates the UI when changed.
