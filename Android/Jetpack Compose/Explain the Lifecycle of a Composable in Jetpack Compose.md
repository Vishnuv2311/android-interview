# Explain the Lifecycle of a Composable in Jetpack Compose

The lifecycle of a composable in Jetpack Compose is tied to the composition process. Understanding this lifecycle helps in building efficient and predictable UIs.

## Phases of a Composable's Lifecycle

1. **Composition**:
   - The composable function is executed to describe the UI.
   - This phase builds the UI tree and determines what needs to be displayed.

2. **Recomposition**:
   - Triggered when the state used by the composable changes.
   - Only the affected parts of the UI tree are re-executed to update the UI.

3. **Decomposition**:
   - Occurs when the composable leaves the composition (e.g., when navigating away or removing the composable).
   - Resources tied to the composable are cleaned up.

---

## Lifecycle-Aware Tools in Jetpack Compose

### 1. `DisposableEffect`
- Used to perform side-effects and cleanup when a composable enters or leaves the composition.
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

### 2. `LaunchedEffect`
- Used to launch coroutines tied to the composable's lifecycle.
```kotlin
@Composable
fun LaunchedEffectExample() {
    LaunchedEffect(Unit) {
        println("LaunchedEffect triggered")
    }
}
```

### 3. `remember`
- Retains state across recompositions but not across configuration changes.
```kotlin
@Composable
fun RememberExample() {
    var counter by remember { mutableStateOf(0) }
    // ...existing code...
}
```

---

## Example: Combining Lifecycle-Aware Tools
```kotlin
@Composable
fun LifecycleExample() {
    var counter by remember { mutableStateOf(0) }

    DisposableEffect(Unit) {
        println("Composable entered composition")
        onDispose {
            println("Composable left composition")
        }
    }

    LaunchedEffect(counter) {
        println("Counter updated: $counter")
    }

    Button(onClick = { counter++ }) {
        Text("Increment")
    }
}
```
- `DisposableEffect` logs when the composable enters and leaves the composition.
- `LaunchedEffect` reacts to changes in the `counter` state.

---

## Key Points
- Composables are lifecycle-aware and adapt to changes in the composition.
- Use tools like `DisposableEffect` and `LaunchedEffect` to handle side-effects and cleanup.
- Keep composables stateless when possible to simplify lifecycle management.

## Summary
The lifecycle of a composable in Jetpack Compose revolves around composition, recomposition, and decomposition. By leveraging lifecycle-aware tools, developers can build efficient and predictable UIs.