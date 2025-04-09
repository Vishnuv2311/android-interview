Dependency Injection (DI) is a design pattern used to achieve Inversion of Control (IoC) between classes and their dependencies. It allows an object to receive its dependencies from an external source rather than creating them itself, making the code more modular, testable, and maintainable.

### Key Points:
- Promotes loose coupling between classes.
- Makes unit testing easier by allowing mock dependencies to be injected.
- Commonly implemented using frameworks like Spring or Guice.

### Types of Dependency Injection:
1. **Constructor Injection**: Dependencies are provided through the class constructor.
2. **Setter Injection**: Dependencies are provided through setter methods.
3. **Interface Injection**: Dependencies are provided through an interface (less common).

### Example (Constructor Injection):

```java
// Service interface
interface Service {
    void performTask();
}

// Implementation of Service
class ServiceImpl implements Service {
    public void performTask() {
        System.out.println("Task performed by ServiceImpl.");
    }
}

// Client class that depends on Service
class Client {
    private Service service;

    // Constructor Injection
    public Client(Service service) {
        this.service = service;
    }

    public void execute() {
        service.performTask();
    }
}

public class Main {
    public static void main(String[] args) {
        // Injecting dependency
        Service service = new ServiceImpl();
        Client client = new Client(service);

        client.execute(); // Output: Task performed by ServiceImpl.
    }
}
```

In the example above, the `Client` class does not create an instance of `ServiceImpl`. Instead, the `Service` dependency is injected into the `Client` class, promoting loose coupling and making the code easier to test and maintain.
