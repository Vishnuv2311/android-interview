# Daemon Threads vs. User Threads

In Java (and consequently in Android), threads are categorized into **User Threads** and **Daemon Threads**.

## User Threads
- These are standard threads that execute until their task is completed.
- They prevent the JVM from exiting if any user thread is still running.
- Ideal for long-running tasks that must complete their execution.

## Daemon Threads
- These are background threads that provide services to user threads.
- The JVM exits when all user threads finish, even if daemon threads are still running.
- Used for low-priority background tasks like garbage collection.

## Key Differences

| Feature         | User Threads       | Daemon Threads  |
|----------------|--------------------|----------------|
| Lifecycle      | Runs independently | Terminates when JVM exits |
| Purpose       | Main program tasks  | Background support tasks |
| JVM Behavior  | JVM waits for them to finish | JVM ignores their state and exits |

## Example Code

```kotlin
fun main() {
    val userThread = Thread {
        println("User thread running...")
        Thread.sleep(5000)
        println("User thread completed.")
    }
    
    val daemonThread = Thread {
        println("Daemon thread running...")
        while (true) { }
    }
    daemonThread.isDaemon = true

    userThread.start()
    daemonThread.start()
}
```

In this example, the **daemon thread** will terminate when the main program finishes execution, whereas the **user thread** ensures completion.
