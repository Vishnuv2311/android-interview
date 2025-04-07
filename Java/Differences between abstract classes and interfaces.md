## Differences between Abstract Classes and Interfaces

| Feature                          | Abstract Class                                   | Interface                                       |
|----------------------------------|--------------------------------------------------|--------------------------------------------------|
| Inheritance                      | Supports single inheritance                      | Supports multiple inheritance                   |
| Access Modifiers                 | Can have public, protected, and private methods  | Methods are public by default                   |
| Method Implementation            | Can have both abstract and concrete methods      | Can have default and static methods (Java 8+)   |
| Fields                           | Can have instance variables                      | Only static final (constants)                   |
| Constructor                      | Can have constructors                            | Cannot have constructors                        |
| Performance                      | Slightly better performance                      | Slightly slower due to dynamic dispatch         |
| Use Case                         | When behavior is common but not identical        | When behavior is expected to be implemented     |
| Keyword                          | Declared with `abstract` keyword                 | Declared with `interface` keyword               |

### Example

**Abstract Class Example**
```java
abstract class Animal {
    abstract void makeSound();
    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

**Interface Example**
```java
interface Flyable {
    void fly();
}
```
