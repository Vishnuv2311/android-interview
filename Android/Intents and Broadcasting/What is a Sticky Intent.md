# What is a Sticky Intent in Android?

A **Sticky Intent** in Android is a special type of intent that remains in the system even after the broadcast is complete. This allows other components to retrieve the data at a later time.

## How Sticky Intents Work
- Sticky Intents are commonly used to broadcast system events such as battery level updates.
- When a broadcast is sent using a sticky intent, it remains in the system so that future receivers can access the most recent data.

## Example of Sending a Sticky Intent
```kotlin
val intent = Intent("com.example.STICKY_ACTION")
intent.putExtra("key", "value")
sendStickyBroadcast(intent)
```

## Example of Receiving a Sticky Intent
```kotlin
val filter = IntentFilter("com.example.STICKY_ACTION")
val stickyIntent = registerReceiver(null, filter)
stickyIntent?.getStringExtra("key")?.let {
    Log.d("StickyIntent", "Received value: $it")
}
```

## Important Notes
- Sticky broadcasts have been **deprecated** since API level 21 (Lollipop) due to security concerns.
- Instead of sticky broadcasts, it is recommended to use alternative mechanisms like `LiveData`, `SharedPreferences`, or local databases.

## Alternatives to Sticky Intents
- **`LocalBroadcastManager`**: Used for local communication within an app.
- **`ViewModel` and `LiveData`**: Preferred for handling UI-related data.
- **`SharedPreferences`** or **Database**: Store persistent data across app sessions.
