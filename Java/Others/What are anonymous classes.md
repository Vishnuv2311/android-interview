### What are Anonymous Classes?

Anonymous classes in Java are a type of inner class without a name. They are used to instantiate and define a class at the same time, typically for one-time use. Anonymous classes are often used when you need to override methods of a class or implement an interface without creating a separate named class.

### Key Characteristics:
- They are declared and instantiated in a single expression.
- They are used to simplify code when a class is needed only once.
- They can extend a class or implement an interface.

### Example:

```java
public class AnonymousClassExample {
    public static void main(String[] args) {
        // Using an anonymous class to implement an interface
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
                System.out.println("Running in an anonymous class!");
            }
        };
        new Thread(runnable).start();

        // Using an anonymous class to extend a class
        Thread thread = new Thread() {
            @Override
            public void run() {
                System.out.println("Thread running in an anonymous class!");
            }
        };
        thread.start();
    }
}
```

### Notes:
- Anonymous classes are concise but can reduce readability if overused.
- Since Java 8, lambda expressions are often preferred over anonymous classes for functional interfaces.
