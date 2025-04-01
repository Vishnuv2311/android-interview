# Difference Between Runnable and Thread in Android

In Android (and Java), both `Runnable` and `Thread` are used to execute code asynchronously, but they have distinct differences.

## 1. Runnable
- `Runnable` is an interface that represents a task that can be executed by a thread.
- It does not create a new thread; instead, it defines a job that a thread will execute.
- A `Runnable` can be passed to multiple threads for execution.
- Implementing `Runnable` is preferred in most cases because it allows better flexibility and separation of concerns.

**Example:**
```kotlin
class MyRunnable : Runnable {
    override fun run() {
        println("Runnable is running")
    }
}

val thread = Thread(MyRunnable())
thread.start()
```

## 2. Thread
- `Thread` is a class that represents an actual thread of execution.
- When you extend `Thread`, a new thread is created and started when you call `start()`.
- However, since Java supports only single inheritance, extending `Thread` limits class extension flexibility.

**Example:**
```kotlin
class MyThread : Thread() {
    override fun run() {
        println("Thread is running")
    }
}

val thread = MyThread()
thread.start()
```

## Key Differences
| Feature | Runnable | Thread |
|---------|---------|--------|
| Type | Interface | Class |
| Execution | Needs to be passed to a `Thread` | Extends `Thread` itself |
| Flexibility | Can be shared across multiple threads | Tightly bound to a single thread |
| Inheritance | Allows extending other classes | Cannot extend other classes |

## Best Practice
- Prefer `Runnable` over extending `Thread`, as it allows for more modular and reusable code.
- Use `Executors` or `HandlerThread` in Android to manage background tasks efficiently.
