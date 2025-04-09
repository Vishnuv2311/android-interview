A static block in Java is executed when the class is loaded into memory by the Java ClassLoader. It is executed only once, before any object of the class is created or any static method is called.

### Key Points:
- Static blocks are used to initialize static variables or perform setup operations.
- They are executed in the order they appear in the class.
- A class can have multiple static blocks.

### Example:

```java
class Example {
    static int value;

    // Static block
    static {
        System.out.println("Static block is executed.");
        value = 42;
    }

    public static void displayValue() {
        System.out.println("Value: " + value);
    }
}

public class Main {
    public static void main(String[] args) {
        // Static block is executed when the class is loaded
        Example.displayValue();
    }
}
```

### Output:
```
Static block is executed.
Value: 42
```

In the example above, the static block is executed when the `Example` class is loaded into memory, initializing the `value` variable before the `displayValue` method is called.
