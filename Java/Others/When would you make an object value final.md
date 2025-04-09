### When Would You Make an Object Value `final`?

In Java, the `final` keyword is used to declare constants or prevent modification of variables, methods, or classes. When applied to an object reference, it ensures that the reference cannot be changed to point to another object, but the object's internal state can still be modified (unless the object itself is immutable).

### Use Cases for Making an Object Value `final`:

1. **To Ensure Reference Immutability**:
   - Use `final` when you want to ensure that the reference to an object cannot be reassigned after initialization.
   - This is useful for constants or objects that should always refer to the same instance.

2. **To Improve Code Readability**:
   - Declaring a variable as `final` makes it clear to other developers that the reference will not change.

3. **To Avoid Accidental Reassignment**:
   - Prevents bugs caused by reassigning a reference to another object.

4. **In Anonymous Classes**:
   - Variables used inside anonymous classes must be effectively `final`.

### Example:

```java
public class FinalExample {
    public static void main(String[] args) {
        final StringBuilder sb = new StringBuilder("Hello");

        // Modifying the internal state is allowed
        sb.append(" World");
        System.out.println(sb); // Output: Hello World

        // Reassigning the reference is not allowed
        // sb = new StringBuilder("New Object"); // Compilation error
    }
}
```

### Notes:
- Use `final` for variables that should not be reassigned.
- For true immutability, use immutable objects (e.g., `String`, custom immutable classes).
- Declaring a variable `final` does not make the object itself immutable.
