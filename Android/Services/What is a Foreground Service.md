# What is a Foreground Service?

A **Foreground Service** in Android is a service that performs an operation noticeable to the user. It must display a notification to keep the user informed about its ongoing task.

## Key Characteristics:
- Runs even when the user is not interacting with the app.
- Displays a persistent notification.
- Ensures the task is less likely to be killed by the system under memory pressure.

## Common Use Cases:
- Music players playing audio.
- Fitness apps tracking activity in real time.
- Download managers handling large file downloads.
- Navigation apps providing turn-by-turn directions.

## How to Start a Foreground Service:
```kotlin
val serviceIntent = Intent(this, MyForegroundService::class.java)
ContextCompat.startForegroundService(this, serviceIntent)
```

## Important Notes:
- Since **Android 9 (API level 28)**, apps cannot start foreground services while in the background.
- Use **WorkManager** for background tasks if a persistent notification is not needed.
- Declare the **FOREGROUND_SERVICE** permission in `AndroidManifest.xml`.

```
<uses-permission android:name="android.permission.FOREGROUND_SERVICE"/>
```

## Example of a Foreground Service:
```kotlin
class MyForegroundService : Service() {
    override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
        val notification = NotificationCompat.Builder(this, CHANNEL_ID)
            .setContentTitle("Foreground Service")
            .setContentText("Running...")
            .setSmallIcon(R.drawable.ic_notification)
            .build()

        startForeground(1, notification)

        return START_STICKY
    }

    override fun onBind(intent: Intent?): IBinder? {
        return null
    }
}
```
