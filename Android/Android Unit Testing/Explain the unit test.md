# Unit Testing in Android

Unit testing is a type of software testing where individual components of a program are tested in isolation to verify their correctness. The main goal of unit testing is to validate that each unit of the software performs as expected.

## Why Unit Testing?
- Ensures code correctness.
- Helps in early bug detection.
- Facilitates refactoring and maintenance.
- Improves overall software quality.

## Unit Testing Frameworks in Android
- **JUnit**: A widely used framework for writing and running unit tests in Java and Kotlin.
- **Mockito**: A popular mocking framework that allows creating and injecting mock dependencies.
- **Robolectric**: A framework that allows running unit tests for Android without an emulator.
  
## Writing a Unit Test Example
Below is an example of a simple unit test using JUnit and Mockito:

```kotlin
import org.junit.Assert.assertEquals
import org.junit.Test

class Calculator {
    fun add(a: Int, b: Int): Int {
        return a + b
    }
}

class CalculatorTest {
    private val calculator = Calculator()

    @Test
    fun testAddition() {
        val result = calculator.add(2, 3)
        assertEquals(5, result)
    }
}
```

## Best Practices for Unit Testing
- Keep tests independent and isolated.
- Use meaningful test names.
- Cover both positive and negative scenarios.
- Use mocking frameworks like Mockito to handle dependencies.
- Run tests frequently.

Unit testing helps in building reliable and maintainable Android applications.
