# How do you find memory leaks in Android applications?

Memory leaks occur when objects are no longer needed but are still referenced, preventing the garbage collector from reclaiming memory. Here are ways to find memory leaks in Android applications:

## 1. Using Android Profiler
- Open **Android Studio** and go to **View > Tool Windows > Profiler**.
- Run the app and select the **Memory Profiler**.
- Look for memory spikes and objects that are not being released.

## 2. LeakCanary Library
- Add LeakCanary dependency in `build.gradle`:
  ```kotlin
  dependencies {
      debugImplementation 'com.squareup.leakcanary:leakcanary-android:2.x'
  }
  ```
- It automatically detects memory leaks and notifies you with a report.

## 3. Analyzing Heap Dumps
- Capture a heap dump using **Android Profiler**.
- Use **MAT (Memory Analyzer Tool)** to analyze retained objects.

## 4. Avoiding Common Memory Leak Causes
- Use `WeakReference` where necessary.
- Avoid holding long-lived references to **Activity**, **Context**, or **View**.
- Unregister listeners, observers, and callbacks in `onDestroy()`.

## 5. Debugging with StrictMode
- Enable **StrictMode** in `Application` class to catch unclosed resources:
  ```kotlin
  class MyApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          StrictMode.setVmPolicy(
              StrictMode.VmPolicy.Builder()
                  .detectLeakedClosableObjects()
                  .penaltyLog()
                  .build()
          )
      }
  }
  ```

By following these methods, you can effectively detect and prevent memory leaks in your Android application.
