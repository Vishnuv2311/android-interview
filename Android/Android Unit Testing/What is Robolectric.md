# What is Robolectric?

Robolectric is a testing framework for Android that allows developers to run unit tests directly on the JVM without requiring an emulator or physical device. It simulates the Android SDK environment, making it faster than traditional instrumentation tests.

## Why Use Robolectric?
- **Fast Execution**: Tests run on the JVM, avoiding the slow emulator/device startup.
- **No Need for Device/Emulator**: Makes testing more accessible in CI/CD pipelines.
- **Access to Android SDK**: Unlike standard JUnit tests, Robolectric provides access to Android framework classes.

## Basic Usage
To use Robolectric, add the following dependency to your `build.gradle`:
```gradle
testImplementation 'org.robolectric:robolectric:4.9'
```

Example test using Robolectric:
```kotlin
@RunWith(RobolectricTestRunner::class)
class ExampleUnitTest {
    @Test
    fun testActivityTitle() {
        val activity = Robolectric.buildActivity(MainActivity::class.java).create().get()
        assertEquals("Expected Title", activity.title)
    }
}
```

## Limitations
- Not a substitute for full instrumentation tests.
- May not support the latest Android APIs immediately.
