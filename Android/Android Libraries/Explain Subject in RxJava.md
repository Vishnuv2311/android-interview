# Subject in RxJava

In RxJava, a `Subject` is a special type of `Observable` that also acts as an `Observer`. This means it can both emit and subscribe to items.

## Types of Subjects in RxJava

1. **PublishSubject**: Emits items to current subscribers only. Subscribers who join later do not receive past items.
2. **BehaviorSubject**: Emits the most recent item (or a default value) to new subscribers and continues emitting new items.
3. **ReplaySubject**: Emits all past and future items to any subscriber.
4. **AsyncSubject**: Emits only the last item (or the completion event) to all subscribers.

## Example Usage

```java
PublishSubject<String> subject = PublishSubject.create();

subject.subscribe(item -> System.out.println("Subscriber 1: " + item));

subject.onNext("Hello");
subject.onNext("RxJava");

subject.subscribe(item -> System.out.println("Subscriber 2: " + item));

subject.onNext("World");
subject.onComplete();
```

## When to Use Subjects
- When bridging non-reactive code with RxJava.
- When multiple subscribers need different behaviors.
- When replaying or caching values is necessary.

Subjects are powerful but should be used with caution to avoid memory leaks and improper state management.
