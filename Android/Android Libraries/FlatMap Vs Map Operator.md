# FlatMap vs Map Operator in RxJava

## Map Operator
The `map` operator in RxJava is used to transform each item emitted by an Observable into another item. It applies a function to each emitted item and emits the transformed result.

### Example:
```kotlin
val observable = Observable.just(2)
    .map { it * 2 }
    .subscribe { println(it) } // Output: 4
```
- `map` is useful when you want to modify emitted items individually without altering the stream structure.

## FlatMap Operator
The `flatMap` operator is used when each emitted item needs to be transformed into another Observable. It flattens multiple emitted Observables into a single Observable.

### Example:
```kotlin
val observable = Observable.just(2)
    .flatMap { num ->
        Observable.just(num * 2, num * 3)
    }
    .subscribe { println(it) } 
// Output: 4, 6
```
- `flatMap` is useful when mapping an item to an Observable that emits multiple items.

## Key Differences:
| Feature  | map | flatMap |
|----------|-----|---------|
| Transformation | One-to-one | One-to-many |
| Output Structure | Same as input | Flattened Observables |
| Concurrency Handling | No concurrency | Supports concurrency |

Use `map` when you want to modify each emitted item individually, and `flatMap` when you need to transform items into new Observables that emit multiple values.
