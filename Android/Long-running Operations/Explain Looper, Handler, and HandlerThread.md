## Looper, Handler, and HandlerThread in Android

### Looper
- Looper is a class that continuously processes messages from a message queue.
- It is used to run a message loop for a thread.
- The main thread in Android has a Looper by default.
- Looper runs an infinite loop to process tasks sequentially.

**Example:**
```kotlin
class MyLooperThread : Thread() {
    lateinit var handler: Handler

    override fun run() {
        Looper.prepare()
        handler = Handler(Looper.myLooper()!!)
        Looper.loop()
    }
}
```

### Handler
- A Handler is used to send and process `Message` or `Runnable` objects associated with a `Looper`.
- It allows communication between background threads and the main thread.

**Example:**
```kotlin
val handler = Handler(Looper.getMainLooper())
handler.post {
    println("Running on UI thread")
}
```

### HandlerThread
- A `HandlerThread` is a specialized thread that has its own Looper.
- It is useful for running background tasks in a separate thread.

**Example:**
```kotlin
val handlerThread = HandlerThread("MyHandlerThread")
handlerThread.start()
val handler = Handler(handlerThread.looper)
handler.post {
    println("Running task in HandlerThread")
}
```

**Summary:**
- `Looper` manages a queue of messages for a thread.
- `Handler` posts tasks/messages to a `Looper`.
- `HandlerThread` creates a thread with its own `Looper`.
