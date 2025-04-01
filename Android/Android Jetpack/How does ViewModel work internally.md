# How does ViewModel work internally?

ViewModel in Android is designed to store and manage UI-related data in a lifecycle-conscious way. It survives configuration changes like screen rotations, preventing the loss of UI-related data.

## Internal Working of ViewModel

1. **ViewModelProvider and ViewModelStore**  
   - The `ViewModelProvider` is responsible for creating and retaining ViewModel instances.
   - `ViewModelStore` holds ViewModel instances and ensures they persist across configuration changes.

2. **Lifecycle Awareness**  
   - ViewModel is scoped to an Activity or Fragment.
   - It does not get destroyed when the Activity is recreated due to configuration changes.

3. **Factory Pattern for Custom ViewModels**  
   - `ViewModelProvider.Factory` is used to create ViewModels with custom constructors.

4. **Clearing ViewModel**  
   - When an Activity or Fragment is permanently destroyed, the ViewModel is cleared.
   - The `onCleared()` method is called to release resources.

## Why Use ViewModel?
- Prevents data loss during configuration changes.
- Decouples UI logic from Activity/Fragment.
- Efficient memory management by avoiding redundant object creation.
