## How to use Android Studio Memory Profiler

The Android Studio Memory Profiler helps developers monitor memory usage, identify memory leaks, and improve app performance.

### Steps to Use:

1. **Launch Your App**  
   Run your app on a real device or emulator in debug mode.

2. **Open the Profiler**  
   Navigate to `View > Tool Windows > Profiler` or click the Profiler tab.

3. **Select the App Process**  
   Choose your app's process to view its performance data.

4. **Use the Memory Profiler**  
   Click the "Memory" section to observe memory usage over time.

5. **Record a Session**  
   Click the record button to start capturing memory activity.

6. **Take a Heap Dump**  
   Click the "Dump Java Heap" button to inspect objects in memory.

7. **Analyze Allocations and Leaks**  
   Use the heap dump and allocation tracking to identify leaks or unusually large memory usage.

8. **Trigger Garbage Collection**  
   Press the "GC" button to force garbage collection and observe its effect.

### Best Practices:

- Monitor memory while performing typical user actions.
- Compare memory usage before and after specific operations.
- Look for memory not being released after activities/fragments are destroyed.
- Combine Memory Profiler with tools like LeakCanary for deeper insight.
