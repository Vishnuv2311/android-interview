# Difference between Dialog and DialogFragment in Android

## Dialog
- `Dialog` is a small window that appears in front of the current activity, used to display alerts, confirmations, or custom UI.
- It is typically created using the `AlertDialog` class or `Dialog` class.
- It is directly tied to the lifecycle of the activity that creates it.
- If the activity is destroyed, the dialog is dismissed and needs to be recreated manually.

## DialogFragment
- `DialogFragment` is a fragment that wraps around a `Dialog` and allows better lifecycle management.
- It is part of the `androidx.fragment.app.DialogFragment` class.
- Unlike `Dialog`, it survives configuration changes like screen rotations.
- It integrates more seamlessly with the fragment lifecycle.
- It is recommended over `Dialog` for better state handling and modularity.

## When to Use Which?
- Use `Dialog` when a simple, short-lived pop-up is needed without fragment dependency.
- Use `DialogFragment` when you need a reusable, lifecycle-aware dialog that integrates well with fragments.

## Example:
**Using `Dialog`**
```kotlin
val dialog = AlertDialog.Builder(this)
    .setTitle("Title")
    .setMessage("This is a dialog")
    .setPositiveButton("OK") { _, _ -> }
    .create()
dialog.show()
```

**Using `DialogFragment`**
```kotlin
class MyDialogFragment : DialogFragment() {
    override fun onCreateDialog(savedInstanceState: Bundle?): Dialog {
        return AlertDialog.Builder(requireContext())
            .setTitle("Title")
            .setMessage("This is a DialogFragment")
            .setPositiveButton("OK") { _, _ -> }
            .create()
    }
}

// Show DialogFragment
MyDialogFragment().show(supportFragmentManager, "dialogFragment")
```
