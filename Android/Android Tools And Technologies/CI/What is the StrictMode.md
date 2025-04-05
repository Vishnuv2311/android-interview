# What is StrictMode in Android?

StrictMode is a developer tool introduced in Android 2.3 (API level 9) that helps developers detect accidental disk or network access on the application's main thread, which can potentially lead to performance issues like ANRs (Application Not Responding).

## Why use StrictMode?

Android enforces a responsive UI. Any long-running operations on the main thread can block user interaction. StrictMode helps catch such operations early during development.

## How to enable StrictMode

StrictMode is typically enabled in the `Application` or `Activity` class within a debug build:

```kotlin
if (BuildConfig.DEBUG) {
    StrictMode.setThreadPolicy(
        StrictMode.ThreadPolicy.Builder()
            .detectDiskReads()
            .detectDiskWrites()
            .detectNetwork()
            .penaltyLog()
            .build()
    )

    StrictMode.setVmPolicy(
        StrictMode.VmPolicy.Builder()
            .detectLeakedSqlLiteObjects()
            .detectLeakedClosableObjects()
            .penaltyLog()
            .penaltyDeath()
            .build()
    )
}
```

## Key Features

- **ThreadPolicy**: Detects disk and network operations on the main thread.
- **VmPolicy**: Detects memory leaks and other violations in the VM.
- **Penalties**: Log violations, flash screen, or even crash the app for violations.

## Best Practices

- Use StrictMode only in development/debug builds.
- Never enable it in production, as it may degrade app performance.
- Review the logs and refactor your code to move heavy operations off the main thread.
