# What is an Explicit Intent?

An Explicit Intent is used to start a specific activity or service within the same application or another application with a known component name.

## Key Characteristics:
- Specifies the exact component (activity, service, or broadcast receiver) to be invoked.
- Used for intra-app navigation (e.g., moving from one activity to another).
- Requires the target component's class name.

## Example:
```kotlin
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)
```

## Use Cases:
- Navigating between activities within the same app.
- Starting a service within the same application.
- Sending data between components.

## Difference from Implicit Intent:
- **Explicit Intent**: Targets a specific component.
- **Implicit Intent**: Declares a general action and lets the system determine the appropriate component.
