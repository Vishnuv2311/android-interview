
 # Android Memory Leak
 
 A memory leak in Android occurs when an object is no longer needed but is still referenced, preventing the garbage collector from reclaiming memory. This can lead to OutOfMemoryErrors and degraded app performance.
 
 ## Common Causes of Memory Leaks
 1. **Static References**: Holding references to Activity or Context in a static field.
 2. **Anonymous Inner Classes & Lambda Expressions**: These can retain references to outer classes.
 3. **Handler and Runnable**: Posting delayed messages without removing them in `onDestroy()`.
 4. **Long-lived Objects**: Singleton instances holding references to Context.
 5. **Observers and Listeners**: Forgetting to unregister listeners.
 6. **Incorrect Use of Fragments**: Holding references to Views after `onDestroyView()`.
 7. **Async Tasks**: Running tasks that outlive their parent Activity.
 
 ## How to Prevent Memory Leaks
 - Use **WeakReference** when holding Activity or Context references.
 - Use **ViewModel** to manage UI-related data lifecycle-aware.
 - Remove callbacks in `onDestroy()`, such as unregistering listeners or clearing Handler messages.
 - Avoid using non-static inner classes in long-lived objects.
 - Use libraries like **LeakCanary** to detect memory leaks in development.
 
 ## Detecting Memory Leaks
 - **LeakCanary**: Automatically detects memory leaks and provides a stack trace.
 - **Android Profiler**: Helps monitor memory usage in Android Studio.
 - **MAT (Memory Analyzer Tool)**: Analyzes heap dumps to find retained objects.
 
 Proper memory management is crucial for ensuring smooth Android app performance and preventing crashes due to excessive memory consumption.