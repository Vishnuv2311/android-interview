# What is Multidex in Android?

**Multidex** in Android is a feature that allows an application to exceed the 64K method limit imposed by the Dalvik Executable (DEX) format. Normally, a single DEX file can contain up to 65,536 methods, and when an app exceeds this limit, it must be split into multiple DEX files.

## Why is Multidex Needed?
- The Dalvik Executable format limits the number of methods in a single DEX file to 65,536 (64K).
- Large applications with many dependencies (such as libraries) can exceed this limit.
- Multidex allows applications to use multiple DEX files, thus overcoming this limitation.

## How to Enable Multidex?
1. **For Applications Running on API Level 21+**  
   Multidex is enabled by default because ART (Android Runtime) supports loading multiple DEX files.

2. **For Applications Running Below API Level 21**  
   - Add the following dependency in `build.gradle`:
     ```gradle
     dependencies {
         implementation 'androidx.multidex:multidex:2.0.1'
     }
     ```
   - Enable multidex in the `defaultConfig` block:
     ```gradle
     android {
         defaultConfig {
             multiDexEnabled true
         }
     }
     ```
   - Extend the `MultiDexApplication` class in your `Application` class:
     ```kotlin
     class MyApp : MultiDexApplication() {
         override fun onCreate() {
             super.onCreate()
             // Initialization code
         }
     }
     ```
   - Alternatively, call `MultiDex.install(this)` in the `attachBaseContext` method:
     ```kotlin
     class MyApp : Application() {
         override fun attachBaseContext(base: Context) {
             super.attachBaseContext(base)
             MultiDex.install(this)
         }
     }
     ```

## Multidex and Performance
- Enabling multidex may increase the startup time due to the need to load multiple DEX files.
- ProGuard and R8 can help reduce method count by removing unused code.
- Using `minSdkVersion 21` avoids legacy multidex overhead, as ART natively supports it.

## Best Practices
- Use **ProGuard/R8** to shrink the method count.
- Remove unused dependencies to keep the method count low.
- If possible, **increase minSdkVersion to 21** to avoid the performance hit of legacy multidex.
