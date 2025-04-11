# How Do You Handle Lifecycle Events in Compose Functions?

Jetpack Compose provides lifecycle-aware tools to handle lifecycle events within composable functions. These tools ensure that side-effects and cleanup operations are performed safely and predictably.

## Tools for Handling Lifecycle Events

### 1. `DisposableEffect`
- Used to perform side-effects when a composable enters or leaves the composition.
- Ideal for setting up and cleaning up resources like listeners or subscriptions.

#### Example:
```kotlin
@Composable
fun DisposableEffectExample() {
    DisposableEffect(Unit) {
        println("Composable entered composition")
        onDispose {
            println("Composable left composition")
        }
    }
}
```
- `onDispose` is called when the composable leaves the composition.

---

### 2. `LaunchedEffect`
- Used to launch coroutines tied to the lifecycle of a composable.
- Automatically cancels the coroutine when the composable leaves the composition.

#### Example:
```kotlin
@Composable
fun LaunchedEffectExample() {
    LaunchedEffect(Unit) {
        println("LaunchedEffect triggered")
        // Perform a one-time operation, e.g., fetching data
    }
}
```

---

### 3. `rememberUpdatedState`
- Ensures that long-lived operations (e.g., coroutines or callbacks) always use the latest value of a state without restarting.

#### Example:
```kotlin
@Composable
fun RememberUpdatedStateExample(onEvent: () -> Unit) {
    val updatedOnEvent by rememberUpdatedState(onEvent)

    LaunchedEffect(Unit) {
        // Safely use the latest onEvent callback
        updatedOnEvent()
    }
}
```

---

### 4. Observing Lifecycle Events
- Use `LocalLifecycleOwner` and `LifecycleEventObserver` to observe lifecycle events explicitly.

#### Example:
```kotlin
@Composable
fun LifecycleObserverExample() {
    val lifecycleOwner = LocalLifecycleOwner.current

    DisposableEffect(lifecycleOwner) {
        val observer = LifecycleEventObserver { _, event ->
            println("Lifecycle event: $event")
        }
        lifecycleOwner.lifecycle.addObserver(observer)
        onDispose {
            lifecycleOwner.lifecycle.removeObserver(observer)
        }
    }
}
```
- This approach is useful for handling specific lifecycle events like `ON_RESUME` or `ON_PAUSE`.

---

## Best Practices
- Use `DisposableEffect` for resource cleanup and setup.
- Use `LaunchedEffect` for lifecycle-aware coroutines.
- Avoid directly observing lifecycle events unless necessary; prefer Compose's lifecycle-aware tools.
- Keep composables stateless when possible to simplify lifecycle management.

---

## Summary
Jetpack Compose provides tools like `DisposableEffect`, `LaunchedEffect`, and `rememberUpdatedState` to handle lifecycle events safely. These tools ensure that side-effects and cleanup operations are tied to the composable's lifecycle, making your code more predictable and efficient.
