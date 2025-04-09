### What Does the `static` Keyword Mean in Java?

In Java, the `static` keyword is used to indicate that a member (variable, method, or block) belongs to the class rather than any specific instance of the class. It can also be used with nested classes.

---

### Key Uses of `static`:

1. **Static Variables**:
   - A `static` variable is shared among all instances of a class.
   - Example:
     ```java
     class Example {
         static int count = 0;
         Example() {
             count++;
         }
     }
     ```

2. **Static Methods**:
   - A `static` method can be called without creating an instance of the class.
   - Example:
     ```java
     class Utility {
         public static int add(int a, int b) {
             return a + b;
         }
     }
     ```

3. **Static Blocks**:
   - A `static` block is used to initialize static variables or execute code during class loading.
   - Example:
     ```java
     class Example {
         static int value;
         static {
             value = 42;
         }
     }
     ```

4. **Static Nested Classes**:
   - A `static` nested class does not require an instance of the outer class.
   - Example:
     ```java
     class Outer {
         static class Nested {
             void display() {
                 System.out.println("Static nested class.");
             }
         }
     }
     ```

---

### Key Points:
- Static members are associated with the class, not instances.
- Static methods cannot access non-static members directly.
- Static blocks are executed once when the class is loaded into memory.
