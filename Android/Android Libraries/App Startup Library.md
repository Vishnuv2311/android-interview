# App Startup Library in Android

The **App Startup Library** is a Jetpack library that provides a straightforward and performant way to initialize components at application startup.

## Features:
- Reduces the need for multiple `ContentProvider` implementations.
- Optimized execution order for initialization tasks.
- Simplifies app startup logic.

## Usage:
To use App Startup, add the dependency:

```gradle
dependencies {
    implementation "androidx.startup:startup-runtime:1.1.1"
}
```

Define an `Initializer`:

```kotlin
class MyInitializer : Initializer<MyDependency> {
    override fun create(context: Context): MyDependency {
        return MyDependency().apply { initialize(context) }
    }

    override fun dependencies(): List<Class<out Initializer<*>>> = emptyList()
}
```

Declare it in `AndroidManifest.xml`:

```xml
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    android:exported="false"
    tools:node="merge">
    <meta-data
        android:name="com.example.MyInitializer"
        android:value="androidx.startup" />
</provider>
```

## Advantages:
- Improves startup time by avoiding unnecessary ContentProviders.
- Manages initialization order efficiently.
- Reduces boilerplate code for app startup logic.

The App Startup Library is ideal for managing dependencies that need initialization at application launch in an optimized manner.
