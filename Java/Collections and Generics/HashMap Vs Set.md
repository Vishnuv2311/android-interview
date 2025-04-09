### HashMap vs HashSet

#### HashMap
- A `HashMap` is a collection that stores key-value pairs.
- Keys in a `HashMap` are unique, but values can be duplicated.
- Allows null keys and null values (only one null key is allowed).
- Provides constant-time performance for basic operations like `put` and `get`.
- Not synchronized, but can be synchronized externally using `Collections.synchronizedMap`.

**Example:**
```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(3, "Cherry");
        map.put(1, "Apricot"); // Overwrites the value for key 1

        System.out.println(map); // Output: {1=Apricot, 2=Banana, 3=Cherry}
    }
}
```

#### HashSet
- A `HashSet` is a collection that stores only unique elements.
- Internally backed by a `HashMap`, where elements are stored as keys with a dummy value.
- Does not allow duplicate elements.
- Allows a single null element.
- Provides constant-time performance for basic operations like `add`, `remove`, and `contains`.
- Not synchronized, but can be synchronized externally using `Collections.synchronizedSet`.

**Example:**
```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Cherry");
        set.add("Apple"); // Duplicate, will not be added

        System.out.println(set); // Output: [Apple, Banana, Cherry]
    }
}
```

#### Key Differences
| Feature           | HashMap                          | HashSet                          |
|--------------------|----------------------------------|----------------------------------|
| Storage            | Key-value pairs                 | Unique elements                 |
| Null Handling      | Allows one null key, multiple null values | Allows one null element         |
| Internal Structure | Uses a hash table               | Backed by a `HashMap`           |
| Synchronization    | Not synchronized                | Not synchronized                |
