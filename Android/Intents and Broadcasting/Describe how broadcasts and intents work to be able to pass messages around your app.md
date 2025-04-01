

 # Broadcasts and Intents in Android
 
 In Android, **Intents** and **Broadcasts** are fundamental mechanisms for communication between components of an application or even across different applications.
 
 ## **What is an Intent?**
 An **Intent** is a messaging object used to request an action from another app component. Intents facilitate interaction between different parts of an application or between different applications.
 
 ### **Types of Intents**
 1. **Explicit Intent** - Used to start a specific component (e.g., launching an activity or service within the same app).
 2. **Implicit Intent** - Used to request an action to be performed by an external app that can handle it (e.g., sharing content or opening a web link).
 
 ## **What is a Broadcast?**
 **Broadcasts** are messages sent by the system or applications to notify interested components about an event. Android provides a mechanism for applications to send or receive these broadcasts.
 
 ### **Types of Broadcasts**
 1. **Normal Broadcasts** - Delivered asynchronously; receivers may not execute in order.
 2. **Ordered Broadcasts** - Delivered in sequence; higher-priority receivers get the message first and can modify or abort it.
 3. **Sticky Broadcasts** *(Deprecated)* - Used to persist broadcast data after it has been sent.
 
 ## **How to Use Broadcasts and Intents**
 - **Sending a Broadcast**:
   ```kotlin
   val intent = Intent("com.example.CUSTOM_ACTION")
   sendBroadcast(intent)
   ```
 
 - **Receiving a Broadcast**:
   ```kotlin
   class MyBroadcastReceiver : BroadcastReceiver() {
       override fun onReceive(context: Context, intent: Intent) {
           Toast.makeText(context, "Broadcast Received!", Toast.LENGTH_SHORT).show()
       }
   }
   ```
 
 - **Registering a Receiver (Dynamically)**:
   ```kotlin
   val receiver = MyBroadcastReceiver()
   val filter = IntentFilter("com.example.CUSTOM_ACTION")
   registerReceiver(receiver, filter)
   ```
 
 ## **Use Cases of Broadcasts**
 - Detecting system events (e.g., battery low, network connectivity changes).
 - Sending app-wide notifications.
 - Triggering background operations based on events.
 
 **Note**: In modern Android versions (API 26+), background broadcasts are restricted. Use `LocalBroadcastManager` or `WorkManager` where necessary.