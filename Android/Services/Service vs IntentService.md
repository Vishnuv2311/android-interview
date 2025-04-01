# Service vs IntentService in Android

## Service
- A `Service` is a component used to perform long-running operations in the background.
- It runs on the **main (UI) thread** by default.
- Developers must manually manage threading using `Thread` or `HandlerThread` to perform background tasks.
- It does **not** stop automatically; it must be stopped manually using `stopSelf()` or `stopService()`.

## IntentService
- An `IntentService` is a subclass of `Service` designed for handling asynchronous tasks in the background.
- It runs on a **separate worker thread** (not the main thread).
- It automatically stops itself when the task is completed.
- Tasks are processed sequentially in a queue using a background thread.

## Key Differences
| Feature           | Service                | IntentService         |
|------------------|----------------------|----------------------|
| Thread Execution | Runs on the main thread | Runs on a worker thread |
| Needs Manual Threading | Yes | No (automatically handled) |
| Stops Automatically | No | Yes (after completing tasks) |
| Task Handling | Can handle multiple tasks concurrently | Processes tasks sequentially |

## When to Use
- Use `Service` when you need background execution that **interacts** with the UI or runs **indefinitely**.
- Use `IntentService` when you need to perform **one-off** background tasks without worrying about threading.
