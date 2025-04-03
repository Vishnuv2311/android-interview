# Designing an LRU (Least Recently Used) Cache

An LRU (Least Recently Used) cache is a data structure that stores a limited number of items and removes the least recently used item when the cache reaches its capacity.

## Key Concepts:
- **Capacity:** The maximum number of elements the cache can hold.
- **Eviction Policy:** When the cache is full, the least recently used item is removed.
- **Operations:** The cache supports `get(key)`, `put(key, value)`, and automatic eviction.

## Implementation:
The LRU cache is typically implemented using:
- A **hashmap (HashMap in Java, LinkedHashMap in Kotlin)** for O(1) lookups.
- A **doubly linked list** to maintain the order of access.

### Code Implementation in Kotlin:
```kotlin
class LRUCache(private val capacity: Int) {
    private val cache = LinkedHashMap<Int, Int>(capacity, 0.75f, true)

    fun get(key: Int): Int {
        return cache[key] ?: -1
    }

    fun put(key: Int, value: Int) {
        if (cache.size >= capacity && !cache.containsKey(key)) {
            val leastUsedKey = cache.keys.iterator().next()
            cache.remove(leastUsedKey)
        }
        cache[key] = value
    }
}
```

### Code Implementation in Java:
```java
import java.util.LinkedHashMap;
import java.util.Map;

class LRUCache {
    private final int capacity;
    private final LinkedHashMap<Integer, Integer> cache;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new LinkedHashMap<>(capacity, 0.75f, true) {
            @Override
            protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
                return size() > capacity;
            }
        };
    }

    public int get(int key) {
        return cache.getOrDefault(key, -1);
    }

    public void put(int key, int value) {
        cache.put(key, value);
    }
}
```

## Time Complexity:
- **Get Operation:** O(1)
- **Put Operation:** O(1)

## Use Cases:
- Web browsers (caching recently visited pages).
- Database caching (storing frequently accessed queries).
- Operating systems (managing memory pages).

This implementation ensures that we efficiently manage frequently accessed data while maintaining optimal performance.
