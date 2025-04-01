# Difference between List and Array types in Kotlin

## List
- `List` is an interface in Kotlin that represents an ordered collection of elements.
- It is immutable by default (`List<T>`), meaning elements cannot be added or removed.
- If mutability is required, use `MutableList<T>`, which allows modifications.
- Commonly used functions: `listOf()`, `mutableListOf()`, `get(index)`, `size`, `add()`, `remove()`, etc.

## Array
- `Array` is a container that holds a fixed number of items of the same type.
- Unlike `List`, the size of an `Array` is fixed at the time of creation.
- Supports both reading and writing elements via index-based access.
- Created using `arrayOf()` or `Array(size) { initializer }`.

## Key Differences
| Feature      | List                   | Array               |
|-------------|-----------------------|---------------------|
| Mutability  | Immutable (`List<T>`), mutable (`MutableList<T>`) | Fixed-size, mutable elements |
| Size        | Dynamic                 | Fixed at creation  |
| Access      | Index-based (`get(index)`) | Index-based (`[index]`) |
| Creation    | `listOf()`, `mutableListOf()` | `arrayOf()`, `Array(size) {}` |
| Performance | Slightly slower (dynamic resizing) | Faster (fixed size) |

## When to Use
- Use `List` when you need a dynamic, resizable collection.
- Use `Array` when you need a fixed-size collection with fast element access.
