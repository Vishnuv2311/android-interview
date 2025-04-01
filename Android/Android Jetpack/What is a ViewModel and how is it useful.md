# What is a ViewModel and how is it useful?

A **ViewModel** is a component of Android Jetpack’s Architecture Components. It is designed to store and manage UI-related data in a lifecycle-conscious way.

## Key Benefits of ViewModel:
- **Survives Configuration Changes**: ViewModel helps retain data during configuration changes like screen rotations.
- **Decouples UI and Business Logic**: It keeps UI controllers (Activities, Fragments) clean and free of business logic.
- **Efficient Data Management**: It caches data and prevents unnecessary data reloads.
- **Works Well with LiveData**: ViewModel can be used with `LiveData` to observe and update UI efficiently.

## Example Usage:
```kotlin
class MyViewModel : ViewModel() {
    private val _text = MutableLiveData&lt;String&gt;()
    val text: LiveData&lt;String&gt; get() = _text

    fun updateText(newText: String) {
        _text.value = newText
    }
}
```

In an Activity or Fragment:
```kotlin
val viewModel: MyViewModel by viewModels()
viewModel.text.observe(viewLifecycleOwner) { newText ->
    textView.text = newText
}
```

## Summary:
ViewModel is a crucial component in modern Android development, improving efficiency and UI state handling.
