# What are "launchMode" in Android?

In Android, `launchMode` is an attribute of the `<activity>` element in the AndroidManifest.xml file that defines how a new instance of an activity is created and how it interacts with the existing activity stack.

There are four types of launch modes:

1. **standard** (default):
   - A new instance of the activity is created every time it is launched.
   - Suitable for independent tasks that don’t require reusing existing instances.

2. **singleTop**:
   - If an instance of the activity already exists at the top of the stack, no new instance is created.
   - Instead, the `onNewIntent()` method is called.

3. **singleTask**:
   - A new task is created, and only one instance of the activity exists in the task.
   - If the activity already exists in the task stack, it is brought to the foreground and `onNewIntent()` is called.

4. **singleInstance**:
   - The activity is the only one in its task, running in isolation.
   - If another activity is started, it will be placed in a separate task.

## Choosing the Right `launchMode`
- Use `standard` for regular activities.
- Use `singleTop` when you want to avoid creating a new instance if the activity is already at the top.
- Use `singleTask` for activities that should always have a single instance, like a home screen.
- Use `singleInstance` for activities that should never have other activities in the same task.

## Example Usage in `AndroidManifest.xml`
```xml
<activity
    android:name=".MainActivity"
    android:launchMode="singleTop"/>
```

This ensures that if `MainActivity` is already running at the top, a new instance is not created.
