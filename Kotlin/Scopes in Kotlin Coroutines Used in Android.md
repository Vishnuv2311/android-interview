# Scopes in Kotlin Coroutines Used in Android

Coroutine scopes in Android help manage the lifecycle of coroutines to avoid memory leaks and ensure that coroutines are canceled when they are no longer needed.

## 1. **GlobalScope**
   - A coroutine launched in `GlobalScope` lives as long as the application.
   - Use it for background tasks that should not be canceled prematurely.
   - **Example:**
     ```kotlin
     GlobalScope.launch {
         delay(1000)
         println("Running in GlobalScope")
     }
     ```

   **⚠️ Avoid using GlobalScope in Android unless necessary, as it is not lifecycle-aware.**

## 2. **lifecycleScope**
   - Introduced in Android Jetpack, it is tied to `LifecycleOwner` (such as an `Activity` or `Fragment`).
   - Coroutines in `lifecycleScope` are automatically canceled when the lifecycle reaches the `DESTROYED` state.
   - **Example:**
     ```kotlin
     class MyActivity : AppCompatActivity() {
         override fun onCreate(savedInstanceState: Bundle?) {
             super.onCreate(savedInstanceState)
             lifecycleScope.launch {
                 fetchData()
             }
         }
     }
     ```

## 3. **viewModelScope**
   - Provided by the Android Architecture Components for `ViewModel`.
   - Coroutines launched within `viewModelScope` are canceled when the `ViewModel` is cleared.
   - **Example:**
     ```kotlin
     class MyViewModel : ViewModel() {
         fun fetchData() {
             viewModelScope.launch {
                 val data = repository.getData()
             }
         }
     }
     ```

## 4. **CoroutineScope with Custom Job**
   - Sometimes, a custom `CoroutineScope` with a `Job` is needed for finer control over coroutines.
   - Example of defining and canceling a custom coroutine scope:
     ```kotlin
     class MyClass {
         private val scope = CoroutineScope(Dispatchers.IO + Job())

         fun fetchData() {
             scope.launch {
                 val result = networkCall()
             }
         }

         fun clear() {
             scope.cancel() // Cancels all coroutines in this scope
         }
     }
     ```

### **Choosing the Right Coroutine Scope in Android**
| Scope            | Tied To            | When to Use |
|-----------------|--------------------|-------------|
| `GlobalScope`   | Application        | Long-running tasks (Use with caution) |
| `lifecycleScope` | LifecycleOwner (Activity/Fragment) | UI-related coroutines that should be auto-canceled |
| `viewModelScope` | ViewModel          | ViewModel-related operations that should persist while the ViewModel is active |
| Custom Scope    | Custom job         | Fine-grained control over coroutine lifetime |

Using the appropriate coroutine scope ensures optimal resource management and avoids memory leaks in Android applications.
