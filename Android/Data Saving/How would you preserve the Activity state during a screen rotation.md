## How to Preserve Activity State During Screen Rotation

When an Android device is rotated, the system destroys and recreates the activity, which can cause the loss of UI state and data. There are several ways to preserve the activity state during screen rotation:

### 1. Using `onSaveInstanceState()`
- Override `onSaveInstanceState(Bundle outState)` to save UI-related data before the activity is destroyed.
- Retrieve the data in `onRestoreInstanceState(Bundle savedInstanceState)` or `onCreate(Bundle savedInstanceState)`.

```kotlin
override fun onSaveInstanceState(outState: Bundle) {
    super.onSaveInstanceState(outState)
    outState.putString("KEY", someValue) // Save necessary data
}

override fun onRestoreInstanceState(savedInstanceState: Bundle) {
    super.onRestoreInstanceState(savedInstanceState)
    val value = savedInstanceState.getString("KEY") // Restore data
}
```

### 2. Using ViewModel
- ViewModel survives configuration changes like screen rotation.
- Ideal for holding UI-related data.

```kotlin
class MyViewModel : ViewModel() {
    val data = MutableLiveData<String>()
}

class MyActivity : AppCompatActivity() {
    private lateinit var viewModel: MyViewModel

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        viewModel = ViewModelProvider(this).get(MyViewModel::class.java)
    }
}
```

### 3. Using `android:configChanges`
- Prevents activity recreation but should be used cautiously.
- Add this in `AndroidManifest.xml`:

```xml
<activity
    android:name=".MyActivity"
    android:configChanges="orientation|screenSize" />
```

- Then handle the configuration change manually in `onConfigurationChanged()`:

```kotlin
override fun onConfigurationChanged(newConfig: Configuration) {
    super.onConfigurationChanged(newConfig)
    // Handle UI updates if necessary
}
```

### 4. Using Retained Fragments (Deprecated in Favor of ViewModel)
- Previously, retained fragments (`setRetainInstance(true)`) were used but are now discouraged.

**Best Practice: Use ViewModel for managing UI-related data and `onSaveInstanceState()` for lightweight data persistence.**
