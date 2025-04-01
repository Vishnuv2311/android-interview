# Different Types of Broadcasts in Android

In Android, Broadcasts are messages that any app can listen to and respond to. There are different types of broadcasts:

## 1. Normal Broadcasts
- Sent to all registered receivers at the same time.
- These broadcasts are not ordered and may be received in any sequence.
- Example: `Intent.ACTION_BATTERY_LOW`.

## 2. Ordered Broadcasts
- Delivered to one receiver at a time in a sequential manner.
- Receivers can propagate or modify the broadcast before passing it to the next receiver.
- Example: A security application receiving a low battery broadcast first and modifying the response.

## 3. Sticky Broadcasts (Deprecated)
- These broadcasts remain in the system after they have been sent.
- Other components can retrieve the last broadcasted intent.
- Example: `Intent.ACTION_BATTERY_CHANGED`.

## 4. Local Broadcasts (Deprecated)
- Used for communication within an app without exposing it to other apps.
- More efficient as it avoids unnecessary inter-process communication.
- Example: Sending a broadcast to update UI components.

## 5. Dynamic and Static Broadcasts
- **Static Broadcasts**: Declared in the AndroidManifest.xml file.
- **Dynamic Broadcasts**: Registered at runtime using `registerReceiver()`.

## Best Practices
- Use **LocalBroadcastManager** alternatives like LiveData, EventBus, or Flow.
- Prefer **dynamic registration** over static to avoid security risks.
- Avoid using sticky broadcasts as they are deprecated.
