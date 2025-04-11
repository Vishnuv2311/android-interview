# What are the Side Effects in Jetpack Compose?

Side effects in Jetpack Compose refer to operations that interact with the external world or persist state beyond the scope of a composable function.

## Purpose of Side Effects
- Composable functions are expected to be pure, meaning they should not produce side effects.
- However, certain operations like logging, launching coroutines, or interacting with external systems require side effects.
- Jetpack Compose provides tools to handle side effects safely and predictably.

## Types of Side Effects

### 1. `LaunchedEffect`
- Used to launch a coroutine tied to the lifecycle of a composable.
- Runs when the key(s) change or when the composable enters the composition.
```kotlin
@Composable
fun LaunchedEffectExample() {
    LaunchedEffect(Unit) {
        // Perform a one-time operation, e.g., fetching data
        println("LaunchedEffect triggered")
    }
}
```

### 2. `rememberCoroutineScope`
- Provides a coroutine scope tied to the composition lifecycle.
- Useful for launching coroutines outside of recomposition.
```kotlin
@Composable
fun RememberCoroutineScopeExample() {
    val scope = rememberCoroutineScope()

    Button(onClick = {
        scope.launch {
            // Perform an operation on button click
            println("Coroutine launched")
        }
    }) {
        Text("Click Me")
    }
}
```

### 3. `DisposableEffect`
- Used to perform cleanup when a composable leaves the composition.
- Runs when the key(s) change or when the composable is removed.
```kotlin
@Composable
fun DisposableEffectExample() {
    DisposableEffect(Unit) {
        println("Effect started")
        onDispose {
            println("Effect cleaned up")
        }
    }
}
```

### 4. `SideEffect`
- Used to perform non-suspending side effects, such as logging or analytics, during recomposition.
```kotlin
@Composable
fun SideEffectExample(counter: Int) {
    SideEffect {
        println("Counter value: $counter")
    }
}
```

### 5. `produceState`
- Converts non-Compose state into Compose state by launching a coroutine.
```kotlin
@Composable
fun ProduceStateExample(): State<String> {
    return produceState(initialValue = "Loading...") {
        delay(1000)
        value = "Data loaded"
    }
}
```

## Best Practices
- Use side-effect APIs provided by Compose to ensure proper lifecycle management.
- Avoid performing side effects directly in composable functions.
- Choose the appropriate side-effect API based on the use case.

## Summary
Side effects in Jetpack Compose allow you to perform operations that go beyond pure UI rendering. By using tools like `LaunchedEffect`, `DisposableEffect`, and `SideEffect`, you can handle side effects in a lifecycle-aware and predictable manner.
