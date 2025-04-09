In Java, exceptions are categorized into **Checked Exceptions** and **Unchecked Exceptions** based on how they are handled during compilation and runtime.

### Checked Exceptions:
- **Definition**: Exceptions that are checked at compile-time.
- **Requirement**: The programmer must handle these exceptions using `try-catch` blocks or declare them in the method signature using `throws`.
- **Examples**: `IOException`, `SQLException`, `FileNotFoundException`.
- **Use Case**: Used for conditions that the program should anticipate and recover from.
- **Example**:
  ```java
  import java.io.*;

  public class CheckedExceptionExample {
      public void readFile() throws IOException {
          FileReader file = new FileReader("file.txt");
          BufferedReader reader = new BufferedReader(file);
          reader.readLine();
      }
  }
  ```

### Unchecked Exceptions:
- **Definition**: Exceptions that are not checked at compile-time.
- **Requirement**: The programmer is not required to handle or declare these exceptions.
- **Examples**: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`.
- **Use Case**: Used for programming errors or conditions that are not expected to be recovered from.
- **Example**:
  ```java
  public class UncheckedExceptionExample {
      public void divideByZero() {
          int result = 10 / 0; // Throws ArithmeticException
      }
  }
  ```

### Key Differences:
| Aspect                | Checked Exceptions                   | Unchecked Exceptions                  |
|-----------------------|---------------------------------------|---------------------------------------|
| **Compile-Time Check**| Checked by the compiler              | Not checked by the compiler           |
| **Handling**          | Must be handled or declared          | Optional to handle                    |
| **Examples**          | `IOException`, `SQLException`        | `NullPointerException`, `ArithmeticException` |
| **Use Case**          | Anticipated recoverable conditions   | Programming errors or logic issues    |

### Summary:
- **Checked Exceptions**: Force the programmer to handle anticipated issues.
- **Unchecked Exceptions**: Indicate programming bugs or unexpected runtime conditions.
