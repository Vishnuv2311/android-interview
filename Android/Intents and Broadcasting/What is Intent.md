# What is Intent in Android?

In Android, an **Intent** is a messaging object used to request an action from another component of the Android system. It facilitates communication between different components, such as activities, services, and broadcast receivers.

## Types of Intents

1. **Explicit Intent** - Specifies the exact component (activity, service, etc.) to be launched.
2. **Implicit Intent** - Declares a general action to be performed, allowing the system to determine the appropriate component.

## Common Use Cases of Intents
- Navigating between activities.
- Starting a service.
- Delivering broadcasts.
- Opening URLs, phone numbers, or other external applications.

## Example of Explicit Intent
```kotlin
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)
```

## Example of Implicit Intent
```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```

Intents are a fundamental part of Android development, enabling seamless interactions between components and applications.
