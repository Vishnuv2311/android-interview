# Instrumented Test in Android

Instrumented tests are tests that run on a real device or an emulator, allowing you to verify the app’s behavior in a real-world environment. These tests have access to Android system APIs, context, and resources.

## Key Features:
- Runs on actual devices/emulators.
- Tests UI interactions, database operations, and real system behaviors.
- Uses `AndroidJUnitRunner` to execute tests.

## How to Write an Instrumented Test:
1. Add the dependency in `build.gradle`:
   ```gradle
   androidTestImplementation 'androidx.test.ext:junit:1.1.5'
   androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
   ```
2. Create a test class in `androidTest`:
   ```kotlin
   @RunWith(AndroidJUnit4::class)
   class ExampleInstrumentedTest {
       @Test
       fun useAppContext() {
           val appContext = InstrumentationRegistry.getInstrumentation().targetContext
           assertEquals("com.example.myapp", appContext.packageName)
       }
   }
   ```

## Best Practices:
- Use Espresso for UI testing.
- Run tests on multiple devices and API levels.
- Mock dependencies to avoid flakiness.

## Running Instrumented Tests:
- Execute in Android Studio via `Run` > `Run 'Tests'`
- Use command line:
  ```
  ./gradlew connectedAndroidTest
  ```

Instrumented tests help ensure app stability across different environments, making them essential for robust Android applications.
