

 # How to Measure Method Execution Time in Android
 
 Measuring method execution time is useful for performance monitoring and optimization. Here are several ways to do it:
 
 ## 1. Using `System.currentTimeMillis()`
 ```kotlin
 val startTime = System.currentTimeMillis()
 // Call the method
 val endTime = System.currentTimeMillis()
 val duration = endTime - startTime
 Log.d("ExecutionTime", "Method executed in $duration ms")
 ```
 
 ## 2. Using `System.nanoTime()`
 ```kotlin
 val startTime = System.nanoTime()
 // Call the method
 val endTime = System.nanoTime()
 val duration = (endTime - startTime) / 1_000_000  // Convert to milliseconds
 Log.d("ExecutionTime", "Method executed in $duration ms")
 ```
 
 ## 3. Using Kotlin's `measureTimeMillis` from `kotlin.system`
 ```kotlin
 import kotlin.system.measureTimeMillis
 
 val duration = measureTimeMillis {
     // Call the method
 }
 Log.d("ExecutionTime", "Method executed in $duration ms")
 ```
 
 ## 4. Using Android Studio Profiler
 - Navigate to `View > Tool Windows > Profiler`.
 - Select your device and app.
 - Record CPU activity to inspect method traces and performance.
 
 ## 5. Using Custom Annotations + Aspect-Oriented Programming (AOP)
 Tools like AspectJ can be used to automatically measure execution time using annotations.
 
 ## Conclusion
 For simple timing, use `measureTimeMillis`. For in-depth analysis, use profiling tools or AOP.