# What is Toast in Android?

A **Toast** in Android is a small message that pops up at the bottom of the screen for a short duration. It is used to provide simple feedback to the user, such as notifications or status messages.

## Features of Toast:
- Does not accept user interaction.
- Automatically disappears after a specified duration.
- Can be customized in terms of duration, position, and appearance.

## Creating a Toast in Android:
Here’s a simple example of how to display a Toast message:

```kotlin
Toast.makeText(context, "Hello, this is a Toast!", Toast.LENGTH_SHORT).show()
```

- `context`: The current application context.
- `"Hello, this is a Toast!"`: The message to be displayed.
- `Toast.LENGTH_SHORT`: Duration (can also be `Toast.LENGTH_LONG`).
- `.show()`: Displays the Toast.

## Custom Toast:
You can also create a custom Toast with a custom layout:

```kotlin
val inflater = layoutInflater
val layout = inflater.inflate(R.layout.custom_toast_layout, findViewById(R.id.toast_root))
val toast = Toast(context)
toast.duration = Toast.LENGTH_LONG
toast.view = layout
toast.show()
```

## Best Practices:
- Use Toasters sparingly to avoid overwhelming the user.
- Consider using `Snackbar` instead of Toast for better UI integration.
