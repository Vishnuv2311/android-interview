# When only onDestroy is called for an Activity without onPause() and onStop()

In Android, the `onDestroy()` method can be called without `onPause()` and `onStop()` under certain rare circumstances. This typically happens in the following scenarios:

## 1. **Finish from `onCreate()`**
   - If an activity calls `finish()` inside `onCreate()`, then `onDestroy()` is called immediately without invoking `onPause()` and `onStop()`.
   - Example:
   ```kotlin
   class MyActivity : AppCompatActivity() {
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           finish() // Activity is finishing immediately
       }
   }
   ```

## 2. **Crash During Creation**
   - If an uncaught exception or an error occurs before the activity completes its initialization, `onDestroy()` may be called directly.

## 3. **Configuration Changes**
   - When an activity is destroyed due to a configuration change (like screen rotation) and `configChanges` is not handled in the manifest, `onDestroy()` may be called without `onPause()` and `onStop()` in some edge cases.

## 4. **Process Kill by the System**
   - If the Android system forcefully kills the process due to memory constraints, `onDestroy()` is called directly without `onPause()` and `onStop()`, as the entire process is being shut down.

These scenarios highlight why it is important not to rely solely on lifecycle methods for critical operations and instead use persistent storage or ViewModels to retain data.
