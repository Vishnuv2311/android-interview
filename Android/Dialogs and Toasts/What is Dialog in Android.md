# What is a Dialog in Android?

A Dialog in Android is a small window that prompts the user to make a decision or enter additional information. It appears in front of the current activity, partially blocking interaction with it.

## Types of Dialogs:
1. **AlertDialog** - Used for displaying alerts and confirmation messages.
2. **ProgressDialog** (Deprecated) - Used to show progress indicators.
3. **DatePickerDialog** - Allows users to select a date.
4. **TimePickerDialog** - Allows users to select a time.
5. **Custom Dialog** - Created using `Dialog` or `DialogFragment` with a custom layout.

## Example:
```kotlin
val builder = AlertDialog.Builder(this)
builder.setTitle("Alert")
    .setMessage("Are you sure?")
    .setPositiveButton("Yes") { dialog, _ -> 
        dialog.dismiss()
    }
    .setNegativeButton("No") { dialog, _ -> 
        dialog.dismiss()
    }
val alertDialog = builder.create()
alertDialog.show()
```

## Best Practices:
- Use `DialogFragment` instead of `Dialog` to avoid memory leaks.
- Ensure dialogs are dismissed properly to prevent window leaks.
- Use `MaterialAlertDialogBuilder` for a modern UI.
