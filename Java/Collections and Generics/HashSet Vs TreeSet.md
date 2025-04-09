HashSet Vs TreeSet

- **HashSet**:
  - Implements the `Set` interface and is backed by a `HashMap`.
  - Does not maintain any order of elements.
  - Allows `null` elements.
  - Offers constant-time performance for basic operations like add, remove, and contains (O(1)).
  - Not synchronized, but can be synchronized externally.

- **TreeSet**:
  - Implements the `NavigableSet` interface and is backed by a `TreeMap`.
  - Maintains elements in sorted (natural or custom) order.
  - Does not allow `null` elements.
  - Offers logarithmic time performance for basic operations like add, remove, and contains (O(log n)).
  - Not synchronized, but can be synchronized externally.

- **Key Differences**:
  - **Order**: HashSet does not maintain order, while TreeSet maintains sorted order.
  - **Performance**: HashSet is faster (O(1)) compared to TreeSet (O(log n)) for most operations.
  - **Null Handling**: HashSet allows one `null` element, whereas TreeSet does not allow `null`.

### Examples

#### HashSet Example
```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> hashSet = new HashSet<>();
        hashSet.add("Apple");
        hashSet.add("Banana");
        hashSet.add("Cherry");
        hashSet.add(null); // HashSet allows null

        System.out.println("HashSet: " + hashSet); // Order is not guaranteed
    }
}
```

#### TreeSet Example
```java
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("Apple");
        treeSet.add("Banana");
        treeSet.add("Cherry");
        // treeSet.add(null); // Throws NullPointerException

        System.out.println("TreeSet: " + treeSet); // Elements are sorted
    }
}
```