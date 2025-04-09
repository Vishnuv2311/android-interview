### Difference between Fail-Fast and Fail-Safe Iterators in Java

1. **Fail-Fast Iterators**:
   - These iterators throw a `ConcurrentModificationException` if the collection is modified while iterating.
   - They operate directly on the collection and detect structural modifications.
   - Examples: Iterators of `ArrayList`, `HashMap`, etc.

2. **Fail-Safe Iterators**:
   - These iterators do not throw exceptions if the collection is modified during iteration.
   - They operate on a cloned copy of the collection, so changes to the original collection are not reflected.
   - Examples: Iterators of `CopyOnWriteArrayList`, `ConcurrentHashMap`, etc.

### Examples

#### Fail-Fast Iterator Example
```java
import java.util.ArrayList;
import java.util.Iterator;

public class FailFastExample {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
            list.add("C"); // This will throw ConcurrentModificationException
        }
    }
}
```

#### Fail-Safe Iterator Example
```java
import java.util.concurrent.CopyOnWriteArrayList;

public class FailSafeExample {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("A");
        list.add("B");

        for (String item : list) {
            System.out.println(item);
            list.add("C"); // No exception will be thrown
        }
    }
}
```
