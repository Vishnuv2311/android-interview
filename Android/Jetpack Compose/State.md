# State in Jetpack Compose

State is a fundamental concept in Jetpack Compose that drives the UI. It represents data that can change over time and triggers recomposition when updated.

## What is State?
- State is any value that can change and needs to be reflected in the UI.
- In Compose, the UI is a function of the state: `UI = f(state)`.

## Types of State
1. **Local State**:
   - Managed within a composable using `remember` or `rememberSaveable`.
   - Example: Counter value in a button click handler.

2. **Shared State**:
   - Managed outside composables, often using a `ViewModel` or other state management tools.
   - Example: App-wide settings or data shared across screens.

## Managing State in Compose

### Using `remember`
- Retains state across recompositions but not across configuration changes.
```kotlin
@Composable
fun RememberExample() {
    var counter by remember { mutableStateOf(0) }

    Button(onClick = { counter++ }) {
        Text("Counter: $counter")
    }
}
```

### Using `rememberSaveable`
- Retains state across recompositions and configuration changes.
```kotlin
@Composable
fun RememberSaveableExample() {
    var counter by rememberSaveable { mutableStateOf(0) }

    Button(onClick = { counter++ }) {
        Text("Counter: $counter")
    }
}
```

### Using `ViewModel`
- For shared or app-wide state, use a `ViewModel` to manage state outside the composable.
```kotlin
class CounterViewModel : ViewModel() {
    var counter by mutableStateOf(0)
        private set

    fun increment() {
        counter++
    }
}

@Composable
fun ViewModelExample(viewModel: CounterViewModel = viewModel()) {
    Button(onClick = { viewModel.increment() }) {
        Text("Counter: ${viewModel.counter}")
    }
}
```

## Best Practices
- Use `remember` for transient state within a composable.
- Use `rememberSaveable` for state that needs to survive configuration changes.
- Use `ViewModel` for shared or app-wide state.
- Keep state localized to the composable that needs it to minimize recomposition scope.

## Summary
State in Jetpack Compose is the driving force behind dynamic and interactive UIs. By managing state effectively, you can create responsive and maintainable applications.
