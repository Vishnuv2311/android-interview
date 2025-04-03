# Observer Design Pattern

## Definition
The Observer Design Pattern is a behavioral design pattern in which an object, called the **subject**, maintains a list of its **observers** and notifies them of any state changes. This pattern is commonly used to implement distributed event-handling systems.

## How It Works
1. The **subject** maintains a list of **observers**.
2. When the state of the subject changes, all **observers** are notified.
3. Observers can subscribe or unsubscribe dynamically.

## Implementation in Java (Android)

### Step 1: Define the Observer Interface
```java
interface Observer {
    void update(String message);
}
```

### Step 2: Create the Subject Interface
```java
import java.util.ArrayList;
import java.util.List;

interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers(String message);
}
```

### Step 3: Implement the Concrete Subject
```java
class NewsPublisher implements Subject {
    private List<Observer> observers = new ArrayList<>();

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}
```

### Step 4: Implement the Concrete Observers
```java
class NewsReader implements Observer {
    private String name;

    public NewsReader(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received news: " + message);
    }
}
```

### Step 5: Test the Pattern
```java
public class ObserverPatternDemo {
    public static void main(String[] args) {
        NewsPublisher publisher = new NewsPublisher();

        Observer reader1 = new NewsReader("Alice");
        Observer reader2 = new NewsReader("Bob");

        publisher.addObserver(reader1);
        publisher.addObserver(reader2);

        publisher.notifyObservers("Breaking News: Observer Pattern in Android!");
    }
}
```

## Use Cases in Android
- **LiveData in MVVM**: ViewModels act as subjects, notifying UI (observers) of changes.
- **EventBus Libraries**: Used for inter-component communication.
- **BroadcastReceivers**: Observers listen for system-wide broadcasts.

## Advantages
- **Loose Coupling**: Observers and subjects interact with minimal dependencies.
- **Dynamic Subscription**: Observers can join or leave at runtime.

## Disadvantages
- **Memory Leaks**: If observers are not unregistered properly.
- **Overhead**: Frequent updates can impact performance.

---
This pattern is widely used in Android to implement reactive programming techniques and event-driven architecture.
