# Why do we need to call `setContentView()` in `onCreate()` of Activity class?

In Android, the `setContentView()` method is called inside the `onCreate()` method of an `Activity` to define the layout for the user interface. Here’s why it is necessary:

## 1. **Binding UI to the Activity**
   - `setContentView()` links the XML layout file to the Activity.
   - Without calling this method, the Activity will not display any UI elements.

## 2. **Inflating the Layout**
   - The method inflates the specified layout resource (`XML file`) and converts it into a `View` hierarchy.
   - This is necessary for the framework to render the UI correctly.

## 3. **Lifecycle Considerations**
   - The `onCreate()` method is the best place to initialize the UI because it is called when the Activity is first created.
   - Placing `setContentView()` here ensures the layout is set before the Activity is displayed to the user.

## 4. **Accessing UI Elements**
   - After calling `setContentView()`, you can use `findViewById()` to get references to UI components.
   - Without setting the content view, `findViewById()` would return `null` since no UI elements would be available.

## 5. **Separation of Concerns**
   - Defining the layout separately in XML and linking it via `setContentView()` ensures a clear separation of UI and logic, making the code more maintainable.

### Example:
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main) // Associates the XML layout with the Activity
    }
}
```

By calling `setContentView()`, we ensure that the UI is properly initialized, displayed, and ready for user interaction.
