# What is UI-Automator?

UI Automator is a UI testing framework provided by Android that allows developers to test user interface interactions across multiple apps. It enables functional UI testing for Android applications, even if they span multiple processes.

## Features of UI Automator
- Allows cross-app testing, enabling interaction with system applications (e.g., Settings, Notifications).
- Uses the `UiDevice` class to simulate user actions such as clicks, swipes, and text input.
- Supports testing without access to application source code.
- Provides access to `AccessibilityNodeInfo` for inspecting the UI hierarchy.
- Can be integrated with Android Instrumentation Testing for end-to-end UI validation.

## Example Usage

```kotlin
@RunWith(AndroidJUnit4::class)
class UiAutomatorTest {

    private lateinit var device: UiDevice

    @Before
    fun setUp() {
        device = UiDevice.getInstance(InstrumentationRegistry.getInstrumentation())
    }

    @Test
    fun testOpenSettings() {
        device.pressHome()
        val settingsApp = device.findObject(UiSelector().text("Settings"))
        settingsApp.click()

        val wifiOption = device.findObject(UiSelector().text("Wi-Fi"))
        assertTrue(wifiOption.exists())
    }
}
```

## When to Use UI Automator?
- When testing UI interactions that span multiple apps.
- When automating interactions with system UI elements.
- When performing end-to-end testing in conjunction with Espresso.

UI Automator is particularly useful for scenarios where automated testing needs to interact with UI elements beyond a single application.
