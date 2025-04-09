### Monitor and Synchronization in Java

1. **Monitor**:
   - A monitor is a synchronization construct that allows threads to have mutual exclusive access to shared resources.
   - In Java, every object has an implicit monitor associated with it.

2. **Synchronization**:
   - Synchronization is the process of controlling access to shared resources by multiple threads to prevent data inconsistency.
   - It ensures that only one thread can execute a synchronized block or method at a time.

### Types of Synchronization

1. **Synchronized Method**:
   - The entire method is synchronized, and the monitor is associated with the object or class.
   - Example:
     ```java
     public synchronized void method() {
         // ...existing code...
     }
     ```

2. **Synchronized Block**:
   - Only a specific block of code is synchronized, allowing finer control.
   - Example:
     ```java
     public void method() {
         synchronized (this) {
             // ...existing code...
         }
     }
     ```

### Example
```java
public class SynchronizationExample {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }

    public static void main(String[] args) throws InterruptedException {
        SynchronizationExample example = new SynchronizationExample();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final Count: " + example.getCount()); // Output: 2000
    }
}
```