The `volatile` modifier in Java is used to indicate that a variable's value will be modified by multiple threads. It ensures visibility and ordering of changes to the variable across threads.

### Key Points:
1. **Visibility**: Changes made to a `volatile` variable by one thread are immediately visible to other threads.
2. **No Caching**: The value of a `volatile` variable is always read from and written to the main memory, bypassing thread-local caches.
3. **Atomicity**: While `volatile` ensures visibility, it does not guarantee atomicity for compound actions (e.g., incrementing a variable).

### Example:
```java
class VolatileExample {
    private volatile boolean flag = true;

    public void stopThread() {
        flag = false; // Change is visible to other threads
    }

    public void run() {
        while (flag) {
            // Thread keeps running until flag is set to false
        }
    }
}
```

### Use Cases:
- Flags or status indicators shared between threads.
- Variables that are read and written by multiple threads without requiring atomic operations.

### Limitations:
- Does not replace synchronization for complex operations.
- Does not guarantee thread safety for non-atomic operations like `count++`.

### Comparison with `synchronized`:
- `volatile` is lightweight and only ensures visibility.
- `synchronized` provides both visibility and atomicity but has higher overhead.

### Example in Android:
```java
public class VolatileFlagExample {
    private volatile boolean isRunning = true;

    public void stop() {
        isRunning = false;
    }

    public void executeTask() {
        new Thread(() -> {
            while (isRunning) {
                // Perform task
            }
        }).start();
    }
}
```

In this example, the `volatile` keyword ensures that changes to `isRunning` are visible across threads.
