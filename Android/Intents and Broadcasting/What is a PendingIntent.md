# What is a PendingIntent in Android?

A `PendingIntent` in Android is a token that you give to another application (such as the system or another app), which allows it to perform an action on your behalf at a later time. It essentially wraps an `Intent` and grants the necessary permissions to execute it even if your application is not running.

## Use Cases
- **Notifications:** Used to execute actions when the user interacts with a notification.
- **Alarms (AlarmManager):** Used to schedule future tasks.
- **Foreground Services:** Helps in starting or stopping a service.
- **Broadcasts:** Used to send intents at a later time.

## Types of PendingIntent
- `PendingIntent.getActivity()`: Starts an `Activity`.
- `PendingIntent.getService()`: Starts a `Service`.
- `PendingIntent.getBroadcast()`: Sends a `Broadcast`.

## Example Usage
```kotlin
val intent = Intent(context, MyActivity::class.java)
val pendingIntent = PendingIntent.getActivity(
    context, 
    0, 
    intent, 
    PendingIntent.FLAG_UPDATE_CURRENT
)
```

## Important Notes
- Always use appropriate flags (`FLAG_UPDATE_CURRENT`, `FLAG_IMMUTABLE`, etc.).
- From Android 12, `FLAG_IMMUTABLE` or `FLAG_MUTABLE` must be explicitly specified.
