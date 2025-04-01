# How can two distinct Android apps interact?

In Android, two distinct apps can interact using the following methods:

## 1. Intents (Implicit and Explicit)
- Apps can send explicit or implicit intents to communicate with other apps.
- Example: Sharing data using `ACTION_SEND` intent.
- Explicit intents are used when the target component is known.
- Implicit intents allow the system to decide which app can handle the request.

```kotlin
val sendIntent = Intent().apply {
    action = Intent.ACTION_SEND
    putExtra(Intent.EXTRA_TEXT, "Hello from App A!")
    type = "text/plain"
}
startActivity(Intent.createChooser(sendIntent, "Share via"))
```

## 2. Content Providers
- Apps can share data using `ContentProvider` and grant specific permissions using URI permissions.
- Example: A notes app exposing data to another app.

```kotlin
val cursor = contentResolver.query(
    Uri.parse("content://com.example.provider/notes"),
    null, null, null, null
)
```

## 3. Bound Services (AIDL)
- `AIDL (Android Interface Definition Language)` allows apps to communicate using IPC (Inter-Process Communication).
- Used for complex interactions like music playback across different apps.

## 4. Broadcast Receivers
- Apps can listen for system or custom broadcasts to receive messages.
- Example: Listening for a broadcast from another app.

```kotlin
val filter = IntentFilter("com.example.SEND_MESSAGE")
registerReceiver(receiver, filter)
```

## 5. PendingIntent
- Allows another app to execute a piece of code on behalf of the original app.
- Commonly used in notifications and alarm managers.

```kotlin
val pendingIntent = PendingIntent.getActivity(
    context, 0, Intent(context, TargetActivity::class.java), PendingIntent.FLAG_UPDATE_CURRENT
)
```

## 6. Deep Linking
- Enables one app to open a specific screen in another app using a URI.

```kotlin
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("myapp://details?id=123"))
startActivity(intent)
```

## 7. Messenger
- A lightweight IPC mechanism used to communicate between services and activities.

These methods enable apps to securely interact while following Android's permission model.
