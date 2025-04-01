# Difference between onCreate() and onStart() in Android

## onCreate()
- Called when the activity is first created.
- Used to initialize essential components, such as UI elements, view bindings, and setting up LiveData or ViewModels.
- Runs only once during the entire lifecycle of the activity, unless the activity is destroyed and recreated.
- Suitable for one-time setup tasks like initializing databases, setting up network connections, or dependency injection.

## onStart()
- Called when the activity becomes visible to the user.
- Runs after `onCreate()` but can be called multiple times during the lifecycle, such as when the activity is resumed after being paused.
- Suitable for tasks related to UI updates, animations, and resource allocations.
- Called every time the activity comes to the foreground.

### Key Differences:
| Feature       | onCreate() | onStart() |
|--------------|-----------|-----------|
| When is it called? | Once when activity is created | Every time activity becomes visible |
| Purpose | Initialization, setting up resources | UI updates, resource allocations |
| Runs again after configuration change? | Yes | Yes |
| Runs after activity resumes from background? | No | Yes |

### Example:

```kotlin
class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        Log.d("Lifecycle", "onCreate called")
    }

    override fun onStart() {
        super.onStart()
        Log.d("Lifecycle", "onStart called")
    }
}
```
