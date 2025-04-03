# Factory Design Pattern

The Factory Design Pattern is a creational pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created.

## Why Use Factory Pattern?
- Encapsulates object creation logic.
- Promotes loose coupling between client code and concrete classes.
- Improves code maintainability and scalability.

## Implementation in Java

```java
// Step 1: Create an interface
interface Vehicle {
    void create();
}

// Step 2: Implement concrete classes
class Car implements Vehicle {
    @Override
    public void create() {
        System.out.println("Car created");
    }
}

class Bike implements Vehicle {
    @Override
    public void create() {
        System.out.println("Bike created");
    }
}

// Step 3: Create the Factory class
class VehicleFactory {
    public static Vehicle getVehicle(String type) {
        if ("Car".equalsIgnoreCase(type)) {
            return new Car();
        } else if ("Bike".equalsIgnoreCase(type)) {
            return new Bike();
        }
        return null;
    }
}

// Step 4: Client code
public class FactoryPatternExample {
    public static void main(String[] args) {
        Vehicle car = VehicleFactory.getVehicle("Car");
        car.create();

        Vehicle bike = VehicleFactory.getVehicle("Bike");
        bike.create();
    }
}
```

## Implementation in Kotlin

```kotlin
// Step 1: Define an interface
interface Vehicle {
    fun create()
}

// Step 2: Implement concrete classes
class Car : Vehicle {
    override fun create() {
        println("Car created")
    }
}

class Bike : Vehicle {
    override fun create() {
        println("Bike created")
    }
}

// Step 3: Create the Factory class
object VehicleFactory {
    fun getVehicle(type: String): Vehicle? {
        return when (type.lowercase()) {
            "car" -> Car()
            "bike" -> Bike()
            else -> null
        }
    }
}

// Step 4: Client code
fun main() {
    val car = VehicleFactory.getVehicle("Car")
    car?.create()

    val bike = VehicleFactory.getVehicle("Bike")
    bike?.create()
}
```

## Use Cases in Android
- **ViewModelProvider.Factory**: Used to create ViewModel instances.
- **Room Database**: DAO instances are created using a factory pattern.
- **WorkManager**: WorkRequest factories are used to instantiate tasks dynamically.

## Advantages
- Centralized object creation.
- Increased flexibility in code maintenance.
- Enhances testability.

## Disadvantages
- Increases complexity if not used appropriately.
- Can make debugging harder due to indirect instantiation.

The Factory Design Pattern is a powerful tool in Android development for managing object creation efficiently.
