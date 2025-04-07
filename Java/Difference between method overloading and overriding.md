## Difference Between Method Overloading and Method Overriding

| Feature                         | Method Overloading                             | Method Overriding                                |
|---------------------------------|--------------------------------------------------|--------------------------------------------------|
| Definition                      | Defining multiple methods with the same name but different parameters within the same class. | Defining a method in a child class with the same signature as in its parent class. |
| Parameters                      | Must be different in type, number, or order.     | Must have the same method signature.             |
| Return Type                    | Can be different.                               | Must be the same or covariant return type.       |
| Inheritance                    | Not required.                                   | Requires inheritance (subclass-parent relation). |
| Polymorphism                   | Compile-time polymorphism (static binding).     | Runtime polymorphism (dynamic binding).          |
| Access Modifiers               | Can have any access modifier.                   | Cannot reduce the visibility of the overridden method. |
| Exceptions                     | No restriction.                                 | Cannot throw new or broader checked exceptions.  |
| Purpose                        | Increases the readability of the program.       | Enables specific implementation in the subclass. |

### Examples:

#### Method Overloading:
```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

#### Method Overriding:
```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}
```
