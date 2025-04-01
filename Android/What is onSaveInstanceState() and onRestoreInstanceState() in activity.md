# What is onSaveInstanceState() and onRestoreInstanceState() in Activity?

## onSaveInstanceState()
`onSaveInstanceState()` is a lifecycle method in Android that is used to save the current state of an activity before it gets destroyed. This is typically used when an activity is temporarily destroyed due to configuration changes (such as screen rotation) or when the system needs to reclaim resources.

### Usage:
```kotlin
override fun onSaveInstanceState(outState: Bundle) {
    super.onSaveInstanceState(outState)
    outState.putString("key", "Some Value")
}
```
This method stores key-value pairs in a `Bundle` object, which can later be retrieved in `onRestoreInstanceState()` or `onCreate()`.

---

## onRestoreInstanceState()
`onRestoreInstanceState()` is called after `onCreate()`, only if the activity is being recreated after being previously destroyed. It is used to restore the state that was saved in `onSaveInstanceState()`.

### Usage:
```kotlin
override fun onRestoreInstanceState(savedInstanceState: Bundle) {
    super.onRestoreInstanceState(savedInstanceState)
    val value = savedInstanceState.getString("key")
}
```
Alternatively, the saved instance state can also be restored inside `onCreate()`.

---

## Key Differences:
| Aspect | onSaveInstanceState() | onRestoreInstanceState() |
|--------|----------------------|------------------------|
| When it is called? | Before the activity is destroyed | After `onCreate()` if there is a saved state |
| Purpose | Saves temporary UI state data | Restores UI state data |
| Parameters | Receives a `Bundle` to store state | Receives a `Bundle` with previously saved state |
| Called when? | Before activity gets destroyed (e.g., due to configuration changes) | When the activity is recreated after destruction |

---

## When to Use?
- Use `onSaveInstanceState()` to persist small UI-related data, such as user input, scroll position, or selected items.
- Use `onRestoreInstanceState()` or check `savedInstanceState` in `onCreate()` to restore the data when the activity is recreated.
