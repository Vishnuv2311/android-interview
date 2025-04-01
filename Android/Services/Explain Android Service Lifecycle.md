

 # Android Service Lifecycle
 
 In Android, a Service is a component that runs in the background to perform long-running operations without a user interface. The service lifecycle consists of the following stages:
 
 ## 1. onCreate()
 - Called when the service is first created.
 - Used for one-time setup procedures such as initializing resources.
 
 ## 2. onStartCommand(Intent intent, int flags, int startId)
 - Called each time a client starts the service using `startService(Intent)`.
 - Returns a value that determines what happens if the system kills the service before it is explicitly stopped:
   - `START_STICKY`: Restarts the service with a null intent.
   - `START_NOT_STICKY`: Does not restart the service after being killed.
   - `START_REDELIVER_INTENT`: Restarts the service with the last intent.
 
 ## 3. onBind(Intent intent)
 - Called when a client binds to the service using `bindService(Intent, ServiceConnection, int)`.
 - Returns an `IBinder` object for interaction.
 - Only applicable to bound services.
 
 ## 4. onUnbind(Intent intent)
 - Called when all clients have disconnected from a bound service.
 
 ## 5. onRebind(Intent intent)
 - Called if a client rebinds to the service after `onUnbind()` was called.
 
 ## 6. onDestroy()
 - Called when the service is no longer needed and is being destroyed.
 - Used to release resources.
 
 ## Service Types
 - **Started Service**: Runs until stopped explicitly.
 - **Bound Service**: Tied to a component lifecycle and stops when all clients unbind.
 
 Services should be carefully managed to avoid unnecessary background resource usage.