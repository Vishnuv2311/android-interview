# Theme in Jetpack Compose

Themes in Jetpack Compose provide a way to define and apply consistent styling across your app.

## What is a Theme?
- A theme is a centralized way to define colors, typography, and shapes for your app.
- It ensures a consistent look and feel across all composables.

## Default Theme
Jetpack Compose provides a default theme that can be customized. The default theme includes:
1. **Colors**: Defines the color palette for light and dark themes.
2. **Typography**: Defines font styles for text.
3. **Shapes**: Defines shapes for UI elements like buttons and cards.

## Customizing the Theme
You can customize the theme by overriding the default values.

### Example:
```kotlin
@Composable
fun MyAppTheme(content: @Composable () -> Unit) {
    val colors = lightColors(
        primary = Color(0xFF6200EE),
        primaryVariant = Color(0xFF3700B3),
        secondary = Color(0xFF03DAC6)
    )

    MaterialTheme(
        colors = colors,
        typography = Typography,
        shapes = Shapes,
        content = content
    )
}
```

- `lightColors` and `darkColors` are used to define color palettes.
- `Typography` and `Shapes` can also be customized similarly.

## Applying the Theme
Wrap your app's composables with the custom theme.

### Example:
```kotlin
@Composable
fun MyApp() {
    MyAppTheme {
        // ...existing code...
        Text("Hello, Theme!", style = MaterialTheme.typography.h6)
        // ...existing code...
    }
}
```

## Accessing Theme Values
You can access theme values using `MaterialTheme`.

### Example:
```kotlin
@Composable
fun ThemedButton() {
    Button(
        onClick = { /* ... */ },
        colors = ButtonDefaults.buttonColors(backgroundColor = MaterialTheme.colors.primary)
    ) {
        Text("Click Me", color = MaterialTheme.colors.onPrimary)
    }
}
```

## Best Practices
- Define a custom theme for your app to maintain consistency.
- Use `MaterialTheme` to access theme values instead of hardcoding styles.
- Support both light and dark themes for better user experience.