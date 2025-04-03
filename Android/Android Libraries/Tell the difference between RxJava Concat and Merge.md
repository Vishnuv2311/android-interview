# Difference between RxJava Concat and Merge

In RxJava, both `concat()` and `merge()` are used to combine multiple Observables, but they operate differently in terms of execution order and concurrency.

## `concat()`
- Ensures that the emissions from the first Observable are completed before subscribing to the next Observable.
- Maintains the order of emissions.
- Sequential execution.
- Suitable for cases where order matters.

**Example:**
```java
Observable.concat(
    Observable.just(1, 2, 3),
    Observable.just(4, 5, 6)
).subscribe(System.out::println);
```
**Output:**
```
1
2
3
4
5
6
```

## `merge()`
- Subscribes to all Observables at the same time.
- The emissions from different Observables may be interleaved.
- Parallel execution.
- Suitable for cases where order does not matter.

**Example:**
```java
Observable.merge(
    Observable.intervalRange(1, 3, 0, 1, TimeUnit.SECONDS),
    Observable.intervalRange(4, 3, 0, 1, TimeUnit.SECONDS)
).subscribe(System.out::println);
```
**Possible Output:**
```
1
4
2
5
3
6
```

## Key Differences:
| Feature     | `concat()` | `merge()` |
|------------|-----------|----------|
| Order Maintained | ✅ Yes | ❌ No |
| Execution Mode | Sequential | Parallel |
| Use Case | When order matters | When order does not matter |
