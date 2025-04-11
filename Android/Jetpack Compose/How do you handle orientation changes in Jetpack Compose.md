# How Do You Handle Orientation Changes in Jetpack Compose?

Jetpack Compose simplifies handling orientation changes by leveraging its declarative and state-driven approach. The UI automatically adapts to configuration changes when state is managed correctly.

## Tools for Handling Orientation Changes

### 1. **`rememberSaveable`**
- Use `rememberSaveable` to retain state across configuration changes like orientation changes.
- It persists state using `SavedStateHandle` or `Bundle`.

#### Example:
```kotlin
@Composable
fun RememberSaveableExample() {
    var counter by rememberSaveable { mutableStateOf(0) }

    Column {
        Text("Counter: $counter")
        Button(onClick = { counter++ }) {
            Text("Increment")
        }
    }
}
```
- The `counter` value persists even after an orientation change.

---

### 2. **`ViewModel`**
- Use a `ViewModel` to manage state that needs to survive configuration changes and be shared across composables.

#### Example:
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
    Column {
        Text("Counter: ${viewModel.counter}")
        Button(onClick = { viewModel.increment() }) {
            Text("Increment")
        }
    }
}
```
- The `ViewModel` retains the `counter` value across orientation changes.

---

### 3. **`LocalConfiguration`**
- Use `LocalConfiguration` to detect orientation and adjust the UI dynamically.

#### Example:
```kotlin
@Composable
fun OrientationExample() {
    val configuration = LocalConfiguration.current

    if (configuration.orientation == Configuration.ORIENTATION_LANDSCAPE) {
        Text("Landscape Mode")
    } else {
        Text("Portrait Mode")
    }
}
```
- The UI adapts based on the current orientation.

---

## Best Practices
- Use `rememberSaveable` for local state that needs to persist across configuration changes.
- Use `ViewModel` for shared or app-wide state.
- Avoid manually handling configuration changes; let Compose and Android handle them automatically.
- Use `LocalConfiguration` only when you need to adjust the UI based on orientation or other configuration changes.

---

## Summary
Jetpack Compose handles orientation changes seamlessly when state is managed correctly using tools like `rememberSaveable` and `ViewModel`. By leveraging `LocalConfiguration`, you can dynamically adjust the UI for different orientations without additional complexity.
