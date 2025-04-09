### What is the Difference Between Using `==` and `.equals` on an Object?

In Java, `==` and `.equals` are used to compare objects, but they serve different purposes.

### `==` Operator:
- The `==` operator compares **references** (memory addresses) of objects.
- It checks whether two references point to the same object in memory.
- For primitive types, `==` compares the actual values.

### `.equals` Method:
- The `.equals` method is used to compare the **contents** (or state) of two objects.
- By default, the `.equals` method in the `Object` class behaves like `==`, but it is often overridden in custom classes (e.g., `String`, `Integer`) to compare meaningful data.

### Example:

```java
public class EqualsVsDoubleEquals {
    public static void main(String[] args) {
        String str1 = new String("Hello");
        String str2 = new String("Hello");

        // Using ==
        System.out.println(str1 == str2); // false, because they are different objects

        // Using .equals
        System.out.println(str1.equals(str2)); // true, because their content is the same

        // Primitive comparison
        int a = 5;
        int b = 5;
        System.out.println(a == b); // true, because primitive values are compared
    }
}
```

### Key Points:
1. Use `==` for reference comparison and primitive types.
2. Use `.equals` for content comparison of objects.
3. Always override `.equals` in custom classes to define meaningful equality.
