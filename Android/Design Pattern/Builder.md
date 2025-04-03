# Builder Design Pattern

The Builder Design Pattern is a creational design pattern that is used to construct complex objects step by step. It helps in creating objects with multiple optional parameters without having to overload constructors.

## When to Use?
- When an object has a large number of optional parameters.
- When the process of object creation involves multiple steps.
- To improve code readability and maintainability.

## Implementation in Java

```java
// Step 1: Create a Product Class
public class Car {
    private String engine;
    private int wheels;
    private boolean sunroof;

    // Private constructor
    private Car(CarBuilder builder) {
        this.engine = builder.engine;
        this.wheels = builder.wheels;
        this.sunroof = builder.sunroof;
    }

    @Override
    public String toString() {
        return "Car [engine=" + engine + ", wheels=" + wheels + ", sunroof=" + sunroof + "]";
    }

    // Step 2: Create the Builder Class
    public static class CarBuilder {
        private String engine;
        private int wheels;
        private boolean sunroof;

        public CarBuilder setEngine(String engine) {
            this.engine = engine;
            return this;
        }

        public CarBuilder setWheels(int wheels) {
            this.wheels = wheels;
            return this;
        }

        public CarBuilder setSunroof(boolean sunroof) {
            this.sunroof = sunroof;
            return this;
        }

        public Car build() {
            return new Car(this);
        }
    }
}

// Step 3: Use the Builder to Create Objects
public class BuilderPatternExample {
    public static void main(String[] args) {
        Car car = new Car.CarBuilder()
                .setEngine("V8")
                .setWheels(4)
                .setSunroof(true)
                .build();
        System.out.println(car);
    }
}
```

## Advantages
- Improves code readability.
- Provides a clear and controlled way to build objects.
- Reduces the need for multiple constructors with different parameters.
- Makes the object immutable once built.

## Disadvantages
- More code needs to be written compared to simple constructors.
- Might not be necessary for small objects with fewer parameters.

The Builder pattern is widely used in Android development for creating complex objects such as `AlertDialog`, `Notification`, and `Glide` image loading.
