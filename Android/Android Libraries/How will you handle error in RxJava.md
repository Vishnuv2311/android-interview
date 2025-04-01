# How to Handle Errors in RxJava

In RxJava, errors can be handled using different operators and strategies to ensure smooth execution without crashing the application.

## 1. onErrorReturn()
This operator allows you to return a default value when an error occurs.
```kotlin
observable
    .onErrorReturn { throwable ->
        "Default Value"
    }
    .subscribe { value -> println(value) }
```

## 2. onErrorResumeNext()
This operator lets you switch to another Observable when an error occurs.
```kotlin
observable
    .onErrorResumeNext(Observable.just("Fallback Data"))
    .subscribe { value -> println(value) }
```

## 3. onExceptionResumeNext()
Similar to `onErrorResumeNext()`, but only works with exceptions, not all Throwables.
```kotlin
observable
    .onExceptionResumeNext(Observable.just("Exception Fallback"))
    .subscribe { value -> println(value) }
```

## 4. retry()
This operator retries the execution if an error occurs.
```kotlin
observable
    .retry(3) // Retries up to 3 times
    .subscribe { value -> println(value) }
```

## 5. retryWhen()
This operator allows retrying based on custom logic.
```kotlin
observable
    .retryWhen { errors ->
        errors.zipWith(Observable.range(1, 3)) { error, retryCount ->
            if (retryCount < 3) Observable.timer(2, TimeUnit.SECONDS) else Observable.error(error)
        }
    }
    .subscribe { value -> println(value) }
```

## 6. doOnError()
This operator allows logging or side-effects on error occurrence.
```kotlin
observable
    .doOnError { throwable -> println("Error occurred: $throwable") }
    .subscribe { value -> println(value) }
```

By using these error-handling strategies, you can ensure the smooth functioning of your RxJava-based application.
