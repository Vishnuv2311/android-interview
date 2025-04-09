The `java.util.concurrent.atomic` package provides classes for atomic operations on single variables. These classes (e.g., `AtomicInteger`, `AtomicLong`, `AtomicReference`) expose a common set of methods to perform thread-safe operations without using explicit synchronization.

### Common Methods:

1. **`get()`**:
   - Retrieves the current value of the atomic variable.
   - Thread-safe and ensures visibility of the latest value.
   - Example:
     ```java
     AtomicInteger atomicInt = new AtomicInteger(10);
     int value = atomicInt.get(); // value = 10
     ```

2. **`set(value)`**:
   - Sets the value of the atomic variable to the specified value.
   - Ensures visibility of the updated value to other threads.
   - Example:
     ```java
     atomicInt.set(20); // Updates the value to 20
     ```

3. **`lazySet(value)`**:
   - Sets the value of the atomic variable but may delay the visibility of the update to other threads.
   - Useful for performance optimization when immediate visibility is not required.
   - Example:
     ```java
     atomicInt.lazySet(30); // Sets the value to 30 with potential delay in visibility
     ```

4. **`compareAndSet(expectedValue, newValue)`**:
   - Atomically sets the value to `newValue` if the current value equals `expectedValue`.
   - Returns `true` if the update was successful, otherwise `false`.
   - Example:
     ```java
     boolean updated = atomicInt.compareAndSet(20, 40); // Updates to 40 if current value is 20
     ```

5. **`weakCompareAndSet(expectedValue, newValue)`**:
   - Similar to `compareAndSet`, but does not guarantee success under contention.
   - May fail spuriously, making it suitable for non-critical operations.
   - Example:
     ```java
     boolean updated = atomicInt.weakCompareAndSet(40, 50); // May or may not update to 50
     ```

### Use Cases:
- **`get` and `set`**: For simple reads and writes with guaranteed visibility.
- **`lazySet`**: For performance optimization when immediate visibility is not critical.
- **`compareAndSet`**: For implementing lock-free algorithms and ensuring atomic updates.
- **`weakCompareAndSet`**: For non-critical updates where occasional failures are acceptable.

These methods enable efficient and thread-safe operations on shared variables without the overhead of synchronization.
