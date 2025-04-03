# Design Pattern used in Android

## Singleton Pattern
The Singleton Pattern ensures that a class has only one instance and provides a global point of access to it. This is particularly useful in dependency management, such as when using Dagger for dependency injection. 

### Example:
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

## Factory Pattern
The Factory Pattern is a creational pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of created objects. This is useful for object creation without specifying the exact class of the object that will be created.

### Example:
```java
public abstract class Shape {
    public abstract void draw();
}

public class Circle extends Shape {
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

public class ShapeFactory {
    public static Shape getShape(String shapeType) {
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        }
        return null;
    }
}
```

## Builder Pattern
The Builder Pattern is used to construct a complex object step by step. It allows for the creation of different representations of an object using the same construction process.

### Example:
```java
public class User {
    private String name;
    private int age;

    private User(UserBuilder builder) {
        this.name = builder.name;
        this.age = builder.age;
    }

    public static class UserBuilder {
        private String name;
        private int age;

        public UserBuilder setName(String name) {
            this.name = name;
            return this;
        }

        public UserBuilder setAge(int age) {
            this.age = age;
            return this;
        }

        public User build() {
            return new User(this);
        }
    }
}
```

## Observer Pattern
The Observer Pattern is a behavioral pattern that defines a one-to-many dependency between objects. When one object changes state, all its dependents are notified automatically. This pattern is commonly used in Android with LiveData and RxJava.

### Example:
```java
public interface Observer {
    void update(String message);
}

public class ConcreteObserver implements Observer {
    @Override
    public void update(String message) {
        System.out.println("Received update: " + message);
    }
}

public class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}
```

## Repository Pattern
The Repository Pattern is used to encapsulate the logic required to access data sources. It serves as an intermediary between the domain and data mapping layers, particularly in the MVVM architecture.

### Example:
```java
public class UserRepository {
    private UserDao userDao;

    public UserRepository(UserDao userDao) {
        this.userDao = userDao;
    }

    public LiveData<User> getUser(int userId) {
        return userDao.getUserById(userId);
    }
}
```

## Adapter Pattern
The Adapter Pattern allows the interface of an existing class to be used as another interface. This is commonly used in RecyclerView to adapt data into a format suitable for display.

### Example:
```java
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.ViewHolder> {
    private List<String> data;

    public MyAdapter(List<String> data) {
        this.data = data;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.item_view, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
        holder.bind(data.get(position));
    }

    @Override
    public int getItemCount() {
        return data.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder {
        public ViewHolder(View itemView) {
            super(itemView);
        }

        public void bind(String item) {
            // Bind data to view
        }
    }
}
```

## Facade Pattern
The Facade Pattern provides a simplified interface to a complex subsystem. It hides the complexities of the system and provides a simpler interface to the client.

### Example:
```java
public class Computer {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;

    public Computer() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }

    public void start() {
        cpu.freeze();
        memory.load(0, hardDrive.read(0, 0));
        cpu.execute();
    }
}
```

## Dependency Injection
Dependency Injection is a design pattern used to implement IoC (Inversion of Control), allowing for better separation of concerns. Dagger and Hilt are popular libraries used for dependency injection in Android.

### Example with Dagger:
```java
@Module
public class NetworkModule {
    @Provides
    public Retrofit provideRetrofit() {
        return new Retrofit.Builder()
                .baseUrl("https://api.example.com")
                .build();
    }
}

@Component(modules = {NetworkModule.class})
public interface AppComponent {
    void inject(MyApplication app);
}
```
