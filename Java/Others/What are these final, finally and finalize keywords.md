### What are `final`, `finally`, and `finalize` Keywords?

In Java, `final`, `finally`, and `finalize` are three distinct keywords with different purposes.

---

### `final` Keyword:
The `final` keyword is used to apply restrictions on variables, methods, and classes.

1. **Final Variable**:
   - A `final` variable cannot be reassigned after it is initialized.
   - Example:
     ```java
     final int x = 10;
     // x = 20; // Compilation error
     ```

2. **Final Method**:
   - A `final` method cannot be overridden by subclasses.
   - Example:
     ```java
     class Parent {
         public final void display() {
             System.out.println("This is a final method.");
         }
     }
     ```

3. **Final Class**:
   - A `final` class cannot be extended.
   - Example:
     ```java
     public final class FinalClass {
         // Class content
     }
     ```

---

### `finally` Block:
The `finally` block is used in exception handling to execute code regardless of whether an exception is thrown or not. It is typically used for cleanup operations.

- Example:
  ```java
  try {
      int result = 10 / 0;
  } catch (ArithmeticException e) {
      System.out.println("Exception caught: " + e.getMessage());
  } finally {
      System.out.println("This block always executes.");
  }
  ```

---

### `finalize()` Method:
The `finalize()` method is called by the garbage collector before an object is destroyed. It is used to perform cleanup operations, but its use is discouraged in modern Java due to unpredictability.

- Example:
  ```java
  protected void finalize() throws Throwable {
      System.out.println("Finalize method called before garbage collection.");
  }
  ```

---

### Difference Between `throw` and `throws` Keywords:

In Java, `throw` and `throws` are used for exception handling but serve different purposes.

1. **`throw` Keyword**:
   - Used to explicitly throw an exception from a method or block of code.
   - Example:
     ```java
     public void checkAge(int age) {
         if (age < 18) {
             throw new IllegalArgumentException("Age must be 18 or older.");
         }
     }
     ```

2. **`throws` Keyword**:
   - Declares the exceptions that a method can throw, informing the caller to handle them.
   - Example:
     ```java
     public void readFile(String filePath) throws IOException {
         FileReader file = new FileReader(filePath);
     }
     ```

---

### Key Differences:
| Keyword   | Purpose                                                                 |
|-----------|-------------------------------------------------------------------------|
| `final`   | Restricts modification of variables, methods, or classes.              |
| `finally` | Ensures a block of code is executed after a `try-catch` block.         |
| `finalize`| Used for cleanup before garbage collection (not recommended anymore).  |
| `throw`   | Used to explicitly throw an exception.                                  |
| `throws`  | Declares exceptions a method might throw to be handled by the caller.  |
