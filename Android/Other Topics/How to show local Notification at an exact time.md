# How to Show Local Notification at an Exact Time in Android

To show a local notification at an exact time, use `AlarmManager` to schedule an alarm and a `BroadcastReceiver` to trigger the notification.

## Steps

1. **Create a BroadcastReceiver to Show the Notification**

```kotlin
class NotificationReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        // ...existing code...
        val notificationManager = context.getSystemService(Context.NOTIFICATION_SERVICE) as NotificationManager
        val channelId = "default_channel"

        // Create notification channel for Android O+
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            val channel = NotificationChannel(channelId, "Default Channel", NotificationManager.IMPORTANCE_DEFAULT)
            notificationManager.createNotificationChannel(channel)
        }

        val notification = NotificationCompat.Builder(context, channelId)
            .setContentTitle("Scheduled Notification")
            .setContentText("This notification was scheduled to show at an exact time.")
            .setSmallIcon(R.drawable.ic_notification)
            .build()

        notificationManager.notify(1, notification)
        // ...existing code...
    }
}
```

2. **Schedule the Notification Using AlarmManager**

```kotlin
fun scheduleNotification(context: Context, triggerAtMillis: Long) {
    val intent = Intent(context, NotificationReceiver::class.java)
    val pendingIntent = PendingIntent.getBroadcast(
        context, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT or PendingIntent.FLAG_IMMUTABLE
    )
    val alarmManager = context.getSystemService(Context.ALARM_SERVICE) as AlarmManager
    alarmManager.setExactAndAllowWhileIdle(AlarmManager.RTC_WAKEUP, triggerAtMillis, pendingIntent)
}
```

- `triggerAtMillis` is the exact time in milliseconds (e.g., from `Calendar.getInstance().apply { ... }.timeInMillis`).

3. **Register the Receiver in AndroidManifest.xml**

```xml
<!-- ...existing code... -->
<receiver android:name=".NotificationReceiver" />
<!-- ...existing code... -->
```

## Notes

- Use `setExactAndAllowWhileIdle` for exact alarms, especially on Android 6.0+ (Doze mode).
- Always create a notification channel for Android O+.
- Make sure to handle permissions for posting notifications on Android 13+.

## Summary

- Use `AlarmManager` to schedule an exact alarm.
- Use a `BroadcastReceiver` to show the notification when the alarm triggers.
- Use `NotificationManager` to display the notification to the user.