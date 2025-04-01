

 # What is a Service in Android?
 
 A Service in Android is a component that performs long-running operations in the background without requiring user interaction. Services can be used to perform tasks such as playing music, handling network transactions, or running scheduled jobs.
 
 ## Types of Services:
 1. **Foreground Service** - Runs with a visible notification and keeps running even when the app is not in the foreground (e.g., music player).
 2. **Background Service** - Runs without user interaction but can be stopped by the system when memory is low.
 3. **Bound Service** - Allows components (such as an Activity) to bind to it and interact with it.
 
 ## Service Lifecycle:
 - `onCreate()`: Called when the service is created.
 - `onStartCommand()`: Called when the service starts.
 - `onBind()`: Called when a component binds to the service.
 - `onDestroy()`: Called when the service is destroyed.
 
 ## Example:
 ```kotlin
 class MyService : Service() {
     override fun onBind(intent: Intent?): IBinder? {
         return null
     }
 
     override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
         // Perform background task
         return START_STICKY
     }
 
     override fun onDestroy() {
         super.onDestroy()
     }
 }
 ```
 
 Services are useful for running background tasks efficiently without affecting the user interface.