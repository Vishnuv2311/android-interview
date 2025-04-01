# What is a Retained Fragment?

A **retained fragment** is a fragment that is retained across configuration changes, such as screen rotations. By default, fragments are destroyed and recreated when an activity is recreated due to a configuration change. However, setting a fragment to be retained allows it to persist and retain its state.

## How to Create a Retained Fragment
You can retain a fragment across configuration changes by calling:
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    retainInstance = true
}
```

**Note:** The `retainInstance` property is deprecated in API level 28. It is now recommended to use `ViewModel` instead of retained fragments.

## Use Case
- Retained fragments are mainly used to hold objects like `ViewModel`, large data structures, or background tasks that should not be recreated on configuration changes.
- They are useful for preserving data without having to manually save and restore it in `onSaveInstanceState()`.

## Alternative Approach
Since `retainInstance` is deprecated, the preferred way to retain data across configuration changes is to use **ViewModel** with `SavedStateHandle`.

```kotlin
class MyViewModel : ViewModel() {
    val data = MutableLiveData<String>()
}
```

And in the Activity or Fragment:
```kotlin
val viewModel: MyViewModel by viewModels()
```

## Conclusion
Retained fragments were once a common way to persist data across configuration changes, but due to their complexity and lifecycle management issues, `ViewModel` is now the recommended approach.
