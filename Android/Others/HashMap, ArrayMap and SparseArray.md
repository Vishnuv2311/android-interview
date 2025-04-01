# HashMap, ArrayMap, and SparseArray in Android

## HashMap
- Part of Java's standard collection framework.
- Stores key-value pairs and allows fast lookups.
- Uses more memory due to auto-boxing when storing primitive types.

## ArrayMap
- Part of Android's support library.
- Optimized for memory usage compared to HashMap.
- Uses an internal array-based structure for better performance with a small number of items.

## SparseArray
- Designed specifically for mapping integer keys to values.
- Avoids auto-boxing of keys, making it more memory-efficient than HashMap.
- Performs better when handling primitive int keys.

## Comparison Table

| Feature       | HashMap       | ArrayMap      | SparseArray  |
|--------------|--------------|--------------|--------------|
| Memory Usage | High         | Moderate     | Low          |
| Performance  | Fast for large data sets | Slower than HashMap but optimized for small sets | Optimized for integer keys |
| Primitive Support | Requires auto-boxing | Requires auto-boxing | No auto-boxing needed |

**Recommendation**:
- Use `HashMap` for large datasets requiring fast lookups.
- Use `ArrayMap` when memory efficiency is a concern for small key-value mappings.
- Use `SparseArray` when working with integer keys for better memory and performance efficiency.
