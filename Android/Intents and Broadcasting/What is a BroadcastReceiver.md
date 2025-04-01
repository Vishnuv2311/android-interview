# What is a BroadcastReceiver in Android?

A **BroadcastReceiver** is an Android component that allows an application to listen for system-wide broadcast messages or intents. These messages can originate from the system or from other applications.

## Key Features:
- Used for event-driven communication in Android.
- Can receive both **system-generated** and **app-specific** broadcasts.
- Operates in the background and does not have a user interface.
- Typically registered in the `AndroidManifest.xml` or dynamically at runtime.

## Example Use Cases:
- Listening for system events like **network connectivity changes, battery level updates, or device boot completion**.
- Receiving **push notifications** via Firebase Cloud Messaging (FCM).
- Detecting **incoming calls or SMS messages**.

## How to Implement a BroadcastReceiver:

**1. Declare in Manifest (Static Registration):**
```xml
<receiver android:name=".MyBroadcastReceiver">
    <intent-filter>
        <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    </intent-filter>
</receiver>
```

**2. Define the Receiver Class:**
```kotlin
class MyBroadcastReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if (intent.action == ConnectivityManager.CONNECTIVITY_ACTION) {
            Toast.makeText(context, "Network connectivity changed", Toast.LENGTH_SHORT).show()
        }
    }
}
```

**3. Register at Runtime (Dynamic Registration):**
```kotlin
val receiver = MyBroadcastReceiver()
val intentFilter = IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION)
registerReceiver(receiver, intentFilter)
```

## Types of Broadcasts:
- **Normal Broadcasts**: Delivered to all receivers at the same time.
- **Ordered Broadcasts**: Delivered sequentially, allowing each receiver to pass data to the next.
- **Local Broadcasts**: Used for inter-app communication within the same application.

## Best Practices:
- Always unregister dynamically registered receivers to prevent memory leaks.
- Prefer **LocalBroadcastManager** for in-app communication to enhance security and performance.
- Use **WakefulBroadcastReceiver** for handling long-running operations.

**Conclusion:**  
The `BroadcastReceiver` is a powerful component for responding to system-wide events efficiently, making it an essential tool in Android app development.
