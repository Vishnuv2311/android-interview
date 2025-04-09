# Arrays vs ArrayLists in Java

## Arrays
- Fixed in size: Once created, the size of an array cannot be changed.
- Can store both primitive types (e.g., `int`, `char`) and objects.
- Syntax: `int[] arr = new int[5];`
- Access elements using index: `arr[0] = 10;`
- Performance: Faster as it is a low-level data structure.
- No built-in methods for operations like adding or removing elements.

## ArrayLists
- Dynamic in size: Can grow or shrink as needed.
- Can only store objects (autoboxing is used for primitives like `int` to `Integer`).
- Syntax: `ArrayList<Integer> list = new ArrayList<>();`
- Access elements using methods: `list.add(10);`
- Performance: Slightly slower due to dynamic resizing and additional overhead.
- Provides built-in methods like `add()`, `remove()`, `contains()`, etc.

## Key Differences
| Feature         | Arrays                          | ArrayLists                     |
|-----------------|---------------------------------|--------------------------------|
| Size            | Fixed                          | Dynamic                       |
| Data Types      | Primitives and Objects         | Objects only                  |
| Performance     | Faster                         | Slower                        |
| Methods         | No built-in methods            | Rich set of utility methods   |
| Syntax          | `int[] arr = new int[5];`      | `ArrayList<Integer> list = new ArrayList<>();` |

## When to Use
- Use **Arrays** when the size is fixed and performance is critical.
- Use **ArrayLists** when the size is dynamic and utility methods are needed.
