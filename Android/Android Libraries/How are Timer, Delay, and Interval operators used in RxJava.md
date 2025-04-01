# How are Timer, Delay, and Interval operators used in RxJava

## Timer Operator
The Timer operator in RxJava is used to create an observable that emits a single item after a specified delay. It is useful for scenarios where you need to perform an action after a certain period of time has passed.

### Usage
The Timer operator can be used to schedule a task to be executed after a delay. It is often used in scenarios like delaying a user action or triggering a timeout.

### Code Example
```java
Observable.timer(5, TimeUnit.SECONDS)
    .subscribe(time -> System.out.println("Timer executed after 5 seconds"));
```

## Delay Operator
The Delay operator is used to postpone the emission of items from an observable by a specified duration. Unlike Timer, it can be applied to any observable, delaying the emission of its items.

### Usage
The Delay operator is useful when you want to introduce a pause before emitting items from an observable. This can be helpful in scenarios like rate limiting or simulating network delays.

### Code Example
```java
Observable.just("Hello", "World")
    .delay(3, TimeUnit.SECONDS)
    .subscribe(item -> System.out.println("Delayed item: " + item));
```

## Interval Operator
The Interval operator creates an observable that emits a sequence of integers at specified intervals. It is often used for creating a timer or a recurring task.

### Usage
The Interval operator is useful for scenarios where you need to perform an action repeatedly at fixed time intervals, such as updating a UI or polling a resource.

### Code Example
```java
Observable.interval(1, TimeUnit.SECONDS)
    .subscribe(time -> System.out.println("Tick: " + time));
```

## Differences
- **Timer** emits a single item after a delay, while **Delay** postpones the emission of items from an existing observable.
- **Interval** emits a sequence of items at regular intervals, making it suitable for repeated tasks.
