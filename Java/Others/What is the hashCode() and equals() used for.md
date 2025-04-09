### What is `hashCode()` and `equals()` Used For?

In Java, `hashCode()` and `equals()` are methods from the `Object` class that are used to compare objects and manage their behavior in hash-based collections like `HashMap`, `HashSet`, and `Hashtable`.

### `equals()` Method:
- The `equals()` method is used to compare the **logical equality** of two objects.
- By default, the `equals()` method in the `Object` class behaves like `==` (reference comparison).
- It is often overridden in custom classes to compare the meaningful state of objects.

### `hashCode()` Method:
- The `hashCode()` method returns an integer hash code that represents the object.
- It is used in hash-based collections to determine the bucket location for storing objects.
- If two objects are equal according to `equals()`, they must have the same `hashCode()`.

### Contract Between `hashCode()` and `equals()`:
1. If two objects are equal (`equals()` returns `true`), their `hashCode()` must be the same.
2. If two objects are not equal, their `hashCode()` may or may not be different.
3. Overriding `equals()` requires overriding `hashCode()` to maintain this contract.

### Example:

```java
import java.util.Objects;

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}

public class HashCodeEqualsExample {
    public static void main(String[] args) {
        Person p1 = new Person("Alice", 25);
        Person p2 = new Person("Alice", 25);

        System.out.println(p1.equals(p2)); // true
        System.out.println(p1.hashCode() == p2.hashCode()); // true
    }
}
```

### Key Points:
- Always override both `equals()` and `hashCode()` together.
- Use `Objects.hash()` to simplify `hashCode()` implementation.
- Proper implementation ensures correct behavior in hash-based collections.
