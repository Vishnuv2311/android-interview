# When to Call Dispose and Clear on CompositeDisposable in RxJava

In RxJava, `CompositeDisposable` is used to manage multiple `Disposable` objects efficiently. It provides two key methods: `dispose()` and `clear()`, which serve different purposes.

## `clear()`
- Removes all disposables from the `CompositeDisposable`, but keeps it active for future use.
- Useful when you want to reset subscriptions without needing to recreate the `CompositeDisposable`.
- Example:
  ```kotlin
  compositeDisposable.clear() // Clears all disposables but the instance remains usable
  ```

## `dispose()`
- Disposes all disposables and marks `CompositeDisposable` as disposed, making it unusable afterward.
- Any further attempts to add disposables will be ignored.
- Use this when you no longer need to manage any subscriptions.
- Example:
  ```kotlin
  compositeDisposable.dispose() // Disposes and makes it unusable
  ```

## When to Use
- **Use `clear()`** when you want to unsubscribe from all observables but still reuse the `CompositeDisposable` instance.
- **Use `dispose()`** when you are completely done with the `CompositeDisposable` and won’t add any new subscriptions.

**Best Practices:**
- Call `clear()` in `onStop()` of an Activity or Fragment.
- Call `dispose()` in `onDestroy()` if the `CompositeDisposable` will no longer be used.
