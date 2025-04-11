# Lifecycle in Jetpack Compose

Jetpack Compose integrates seamlessly with the Android lifecycle, ensuring that composables behave correctly as the lifecycle changes.

## Relationship with Android Lifecycle
- Composables are lifecycle-aware and automatically adapt to lifecycle changes.
- They are tied to the lifecycle of the `Activity` or `Fragment` hosting them.

## Lifecycle-Aware Composables
Jetpack Compose provides tools to handle lifecycle events and perform actions accordingly.

### 1. `DisposableEffect`
- Used to perform side-effects that need cleanup when the composable leaves the composition.
- Example:
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

### 2. `LaunchedEffect`
- Used to launch coroutines tied to the lifecycle of a composable.
- Example:
```kotlin
@Composable
fun LaunchedEffectExample() {
    LaunchedEffect(Unit) {
        println("LaunchedEffect triggered")
    }
}
```

### 3. `rememberCoroutineScope`
- Provides a coroutine scope tied to the composable's lifecycle.
- Example:
```kotlin
@Composable
fun RememberCoroutineScopeExample() {
    val scope = rememberCoroutineScope()

    Button(onClick = {
        scope.launch {
            println("Coroutine launched")
        }
    }) {
        Text("Click Me")
    }
}
```

## Handling Lifecycle Events
You can observe lifecycle events using `LifecycleOwner` and `LifecycleEventObserver`.

### Example:
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

## Best Practices
- Use lifecycle-aware APIs like `LaunchedEffect` and `DisposableEffect` for side-effects.
- Avoid directly observing lifecycle events unless necessary.
- Keep composables stateless and delegate state management to `ViewModel` or other lifecycle-aware components.

## Summary
Jetpack Compose simplifies lifecycle management by providing lifecycle-aware APIs. These tools ensure that composables behave predictably and efficiently as the lifecycle changes.
