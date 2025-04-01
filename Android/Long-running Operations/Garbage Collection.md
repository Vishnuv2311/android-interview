

# Garbage Collection in Android

Garbage Collection (GC) is the process of automatically reclaiming memory occupied by objects that are no longer in use, helping to prevent memory leaks and optimize performance.

## How Garbage Collection Works
- The **Dalvik Virtual Machine (DVM)** and later the **Android Runtime (ART)** use GC to manage memory.
- The GC identifies objects that are no longer referenced and reclaims the memory for future allocations.
- The **GC roots** (e.g., active threads, static fields, JNI references) determine which objects are still reachable.

## Types of Garbage Collection in Android
- **Generational Garbage Collection**: Separates short-lived and long-lived objects to improve efficiency.
- **Concurrent Mark and Sweep (CMS)**: Used in Dalvik, minimizes pause times.
- **G1 Garbage Collector**: Introduced in ART for improved performance.
- **ZGC/Shenandoah**: Experimental, focusing on low-latency GC.

## Performance Considerations
- Frequent GC can cause UI jank and slow performance.
- **Avoid memory leaks** by properly releasing resources (e.g., unregistering listeners).
- Use **profiling tools** like Android Studio Profiler to monitor memory usage.
- Prefer **object pooling** for frequently used objects to reduce GC pressure.

## Best Practices to Reduce GC Overhead
- Use **weak references** when necessary (e.g., WeakReference, SoftReference).
- Avoid unnecessary object creation inside loops.
- Prefer **StringBuilder** over String concatenation.
- Release resources (e.g., bitmaps, listeners) when they are no longer needed.
- Use Kotlin’s `by lazy` or `lateinit` for efficient memory management.