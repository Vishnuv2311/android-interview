In Java, copying an object can be done in two ways: **Shallow Copy** and **Deep Copy**. These approaches differ in how they handle the object's fields, especially when the fields are references to other objects.

### Shallow Copy:
- **Definition**: A shallow copy creates a new object, but it copies only the references of the fields to the original objects, not the actual objects themselves.
- **Behavior**: Changes made to the referenced objects in the copied object will reflect in the original object.
- **Use Case**: Suitable when the object contains only primitive fields or immutable objects.
- **Example**:
  ```java
  class ShallowCopyExample implements Cloneable {
      int value;
      int[] array;

      public ShallowCopyExample(int value, int[] array) {
          this.value = value;
          this.array = array;
      }

      @Override
      protected Object clone() throws CloneNotSupportedException {
          return super.clone(); // Performs shallow copy
      }
  }

  public class Main {
      public static void main(String[] args) throws CloneNotSupportedException {
          int[] array = {1, 2, 3};
          ShallowCopyExample original = new ShallowCopyExample(10, array);
          ShallowCopyExample copy = (ShallowCopyExample) original.clone();

          copy.array[0] = 99; // Modifies the original object's array
          System.out.println(original.array[0]); // Output: 99
      }
  }
  ```

### Deep Copy:
- **Definition**: A deep copy creates a new object and also recursively copies all objects referenced by the fields of the original object.
- **Behavior**: Changes made to the referenced objects in the copied object do not affect the original object.
- **Use Case**: Suitable when the object contains mutable fields or nested objects.
- **Example**:
  ```java
  class DeepCopyExample implements Cloneable {
      int value;
      int[] array;

      public DeepCopyExample(int value, int[] array) {
          this.value = value;
          this.array = array;
      }

      @Override
      protected Object clone() throws CloneNotSupportedException {
          DeepCopyExample copy = (DeepCopyExample) super.clone();
          copy.array = array.clone(); // Creates a deep copy of the array
          return copy;
      }
  }

  public class Main {
      public static void main(String[] args) throws CloneNotSupportedException {
          int[] array = {1, 2, 3};
          DeepCopyExample original = new DeepCopyExample(10, array);
          DeepCopyExample copy = (DeepCopyExample) original.clone();

          copy.array[0] = 99; // Does not modify the original object's array
          System.out.println(original.array[0]); // Output: 1
      }
  }
  ```

### Key Differences:
| Aspect                | Shallow Copy                         | Deep Copy                             |
|-----------------------|---------------------------------------|---------------------------------------|
| **Field Copying**     | Copies references of objects         | Copies actual objects recursively     |
| **Independence**      | Changes in copied object affect the original | Changes in copied object do not affect the original |
| **Performance**       | Faster, less memory-intensive        | Slower, more memory-intensive         |
| **Use Case**          | Immutable or primitive fields        | Mutable or nested objects             |

### Summary:
- **Shallow Copy**: Quick and memory-efficient but shares references.
- **Deep Copy**: Ensures complete independence but is more resource-intensive.
