In Java, the `try`, `catch`, and `finally` blocks are used for exception handling, ensuring that runtime errors are properly managed and resources are cleaned up.

### How They Work:

1. **`try` Block**:
   - Contains the code that might throw an exception.
   - If an exception occurs, the control is transferred to the appropriate `catch` block.
   - Example:
     ```java
     try {
         int result = 10 / 0; // This will throw an ArithmeticException
     }
     ```

2. **`catch` Block**:
   - Handles the exception thrown in the `try` block.
   - You can have multiple `catch` blocks to handle different types of exceptions.
   - Example:
     ```java
     catch (ArithmeticException e) {
         System.out.println("Cannot divide by zero: " + e.getMessage());
     }
     ```

3. **`finally` Block**:
   - Always executes after the `try` block, regardless of whether an exception was thrown or caught.
   - Used for cleanup operations like closing files, releasing resources, etc.
   - Example:
     ```java
     finally {
         System.out.println("Execution completed.");
     }
     ```

### Example Code:
```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // Throws ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Exception caught: " + e.getMessage());
        } finally {
            System.out.println("Finally block executed.");
        }
    }
}
```

### Key Points:
- **Order of Execution**:
  1. The `try` block is executed.
  2. If an exception occurs, the corresponding `catch` block is executed.
  3. The `finally` block is executed after the `try` or `catch` block.

- **Multiple `catch` Blocks**:
  - You can have multiple `catch` blocks to handle different exceptions.
  - Example:
    ```java
    try {
        // ...existing code...
    } catch (NullPointerException e) {
        // Handle NullPointerException
    } catch (ArithmeticException e) {
        // Handle ArithmeticException
    }
    ```

- **`finally` Without `catch`**:
  - A `finally` block can be used without a `catch` block if you only need cleanup.
  - Example:
    ```java
    try {
        // ...existing code...
    } finally {
        // Cleanup code
    }
    ```

### Use Cases:
- **`try`**: To wrap code that might throw exceptions.
- **`catch`**: To handle specific exceptions and prevent program termination.
- **`finally`**: To ensure cleanup actions are performed, like closing files or releasing locks.