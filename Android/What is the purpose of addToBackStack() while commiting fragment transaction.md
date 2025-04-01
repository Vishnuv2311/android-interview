# What is the purpose of addToBackStack() while committing a fragment transaction?

## Overview
The `addToBackStack()` method in Android is used during a fragment transaction to allow the user to navigate back to the previous fragment when pressing the back button. Without adding a transaction to the back stack, the previous fragment will not be restored after replacing or removing it.

## Purpose
1. **Back Navigation Support**: When a fragment is replaced or removed, `addToBackStack()` ensures that the previous fragment remains in the back stack, allowing the user to navigate back using the back button.
2. **State Management**: It helps maintain the correct state of fragments, enabling a seamless transition between screens without losing previous states.
3. **Better User Experience**: Enhances the user experience by allowing fragment-based navigation similar to activity-based navigation.
4. **Flexible UI Management**: It enables implementing multi-step flows where users can navigate forward and backward within the same activity.

## Example Usage
```kotlin
val fragmentTransaction = supportFragmentManager.beginTransaction()
fragmentTransaction.replace(R.id.fragment_container, NewFragment())
fragmentTransaction.addToBackStack(null) // Adds transaction to the back stack
fragmentTransaction.commit()
```

## Behavior Without addToBackStack()
If `addToBackStack()` is not used, replacing a fragment will remove the previous fragment from the fragment manager. Pressing the back button will not bring back the previous fragment, and the activity may close instead.

## When to Use?
- When you want users to navigate back to the previous fragment.
- When maintaining a multi-step workflow.
- When dynamically switching between fragments without losing their state.

## When Not to Use?
- If you don’t want the user to navigate back to the previous fragment.
- If fragments are used for temporary UI components that don’t require back navigation.
