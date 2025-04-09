The `synchronized` keyword in Java is used to control access to a block of code or a method by multiple threads. It ensures that only one thread can execute the synchronized block or method at a time, providing thread safety.

### Key Points:
1. **Synchronized Methods**: When a method is declared as `synchronized`, the thread acquires the intrinsic lock (monitor) of the object before executing the method. For static synchronized methods, the lock is on the class object.
   ```java
   public synchronized void instanceMethod() {
       // Thread-safe code
   }

   public static synchronized void staticMethod() {
       // Thread-safe code
   }
   ```

2. **Synchronized Blocks**: Instead of synchronizing an entire method, you can synchronize a specific block of code to improve performance by reducing the scope of the lock.
   ```java
   public void method() {
       synchronized (this) {
           // Thread-safe code
       }
   }
   ```

3. **Intrinsic Locks**: Every object in Java has an intrinsic lock (monitor). A thread must acquire this lock to execute synchronized code.

4. **Reentrancy**: Java's synchronization is reentrant, meaning a thread can acquire the same lock multiple times without causing a deadlock.

5. **Drawbacks**: Overusing synchronization can lead to performance issues due to thread contention and potential deadlocks if not used carefully.

### Use Cases:
- Protecting shared resources (e.g., variables, collections) from concurrent modification.
- Ensuring consistent state in multithreaded environments.

### Example:
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}
```
In this example, the `increment` and `getCount` methods are synchronized to ensure thread-safe access to the `count` variable.
