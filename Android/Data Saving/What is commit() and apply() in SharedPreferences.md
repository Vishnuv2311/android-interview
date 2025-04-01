## commit() vs apply() in SharedPreferences

SharedPreferences in Android provides two methods to save data: `commit()` and `apply()`. 

### commit()
- Synchronously writes data to SharedPreferences.
- Returns a boolean indicating success or failure.
- Blocks the calling thread until the operation is complete.
- Useful when you need immediate confirmation of the operation's success.

### apply()
- Asynchronously writes data to SharedPreferences.
- Does not return any result.
- Writes are batched and handled in the background.
- Recommended for most use cases to avoid blocking the UI thread.

### When to use which?
- Use `commit()` when you need confirmation that the data has been written (e.g., critical user settings).
- Use `apply()` for performance reasons when immediate confirmation isn't necessary.
