# What is Activity and its Lifecycle?

## What is an Activity?
An **Activity** in Android represents a single screen with a user interface. It acts as an entry point for users to interact with an application. An application can have multiple activities, each designed to perform a specific function. Activities work together to provide a seamless user experience.

## Activity Lifecycle
The **Activity Lifecycle** is a set of defined states that an activity goes through from creation to destruction. The Android system manages these states to optimize memory and performance.

### 1. **onCreate()**
   - Called when the activity is first created.
   - Used for initializing components, setting up UI elements, and restoring saved state.
   - Example:
     ```kotlin
     override fun onCreate(savedInstanceState: Bundle?) {
         super.onCreate(savedInstanceState)
         setContentView(R.layout.activity_main)
     }
     ```

### 2. **onStart()**
   - Called when the activity becomes visible to the user.
   - The activity is now in the foreground but may not be interactive.

### 3. **onResume()**
   - Called when the activity starts interacting with the user.
   - The activity is now in the foreground and receives user input.
   - It is the active running state.

### 4. **onPause()**
   - Called when another activity comes into the foreground.
   - The activity is still visible but partially obscured.
   - Used to pause ongoing tasks such as animations, video playback, etc.

### 5. **onStop()**
   - Called when the activity is no longer visible to the user.
   - Used to release resources that are no longer needed.

### 6. **onDestroy()**
   - Called when the activity is about to be destroyed.
   - Used for final clean-up.

### 7. **onRestart()**
   - Called when the activity is stopped and is about to start again.

## Activity Lifecycle Diagram
Below is a simplified representation of the Activity Lifecycle:

```
onCreate() → onStart() → onResume()
onPause() → onStop() → onRestart() → onStart() → onResume()
onPause() → onStop() → onDestroy()
```

Understanding the activity lifecycle is crucial for handling state changes properly, optimizing performance, and avoiding memory leaks.
