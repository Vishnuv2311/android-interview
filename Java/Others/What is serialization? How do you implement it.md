### What is Serialization?

Serialization is the process of converting an object's state into a byte stream so that it can be persisted to a file, sent over a network, or stored in a database. The byte stream can later be deserialized to recreate the original object.

### How to Implement Serialization in Java?

1. **Implement the `Serializable` Interface**: The class whose objects need to be serialized must implement the `java.io.Serializable` interface. This is a marker interface and does not contain any methods.

2. **Use `ObjectOutputStream` to Serialize**: Use `ObjectOutputStream` to write the object to an output stream.

3. **Use `ObjectInputStream` to Deserialize**: Use `ObjectInputStream` to read the object from an input stream.

### Example:

```java
import java.io.*;

class Person implements Serializable {
    private static final long serialVersionUID = 1L; // Recommended for version control
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Person person = new Person("John Doe", 30);

        // Serialization
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
            System.out.println("Object serialized successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialization
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) ois.readObject();
            System.out.println("Deserialized Object: " + deserializedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### Notes:
- Always declare a `serialVersionUID` for a `Serializable` class to ensure compatibility during deserialization.
- Transient fields are not serialized. Use the `transient` keyword for fields that should not be part of the serialized state.
