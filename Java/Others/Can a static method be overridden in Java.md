In Java, static methods cannot be overridden. This is because static methods are associated with the class rather than any specific instance of the class. When you define a static method with the same name and parameters in a subclass, it is called method hiding, not overriding.

### Key Points:
- Static methods belong to the class, not the instance.
- Method overriding is based on runtime polymorphism, which does not apply to static methods.
- Static methods are resolved at compile-time, while overridden methods are resolved at runtime.

### Example:

```java
class Parent {
    static void display() {
        System.out.println("Static method in Parent class");
    }
}

class Child extends Parent {
    static void display() {
        System.out.println("Static method in Child class");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();
        Parent child = new Child();

        parent.display(); // Output: Static method in Parent class
        child.display();  // Output: Static method in Parent class
    }
}
```

In the example above, the `display` method in the `Child` class hides the `display` method in the `Parent` class. However, the method call is resolved based on the reference type, not the object type, demonstrating that static methods are not overridden.
