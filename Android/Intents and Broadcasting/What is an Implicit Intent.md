# What is an Implicit Intent?

An **Implicit Intent** in Android is used to request an action from another app component without specifying the exact component to handle the request. Instead of defining the target explicitly, an implicit intent specifies an action to be performed and optionally includes data related to that action.

## Key Components of an Implicit Intent:
- **Action**: Specifies what the intent should do (e.g., `Intent.ACTION_VIEW`, `Intent.ACTION_SEND`).
- **Data**: URI that represents the data to be processed.
- **Category** (Optional): Provides additional information about the type of component that should handle the intent.
- **Extras** (Optional): Additional key-value data sent with the intent.

## Example of an Implicit Intent:
```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```
This intent opens a web browser to display the specified URL.

## Common Use Cases:
- Opening a webpage in a browser.
- Sharing content via social media or email.
- Dialing a phone number.
- Opening a map location.

## Resolving an Implicit Intent:
Since multiple apps may handle an implicit intent, the system presents a chooser if more than one is available:
```kotlin
val intent = Intent(Intent.ACTION_SEND)
intent.type = "text/plain"
intent.putExtra(Intent.EXTRA_TEXT, "Hello, check this out!")
startActivity(Intent.createChooser(intent, "Share via"))
```

## Difference Between Implicit and Explicit Intent:
- **Explicit Intent**: Specifies the exact component (activity, service, or receiver) to handle the intent.
- **Implicit Intent**: Specifies only the action to be performed, and the system determines the best component to handle it.
