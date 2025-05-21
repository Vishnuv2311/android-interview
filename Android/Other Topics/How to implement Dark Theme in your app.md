# How to Implement Dark Theme in Your App

Supporting Dark Theme improves user experience and accessibility. Android provides built-in support for dark mode in both View-based and Jetpack Compose apps.

## For View-Based Apps

### 1. Define Dark Theme Resources
- Create a `values-night` resource directory.
- Add `colors.xml`, `styles.xml`, and other resources with dark theme values.

```
res/values/colors.xml
res/values-night/colors.xml
res/values/styles.xml
res/values-night/styles.xml
```

### 2. Use Theme Attributes
- Reference colors and styles using theme attributes (e.g., `?attr/colorPrimary`).

### 3. Opt-In to Dark Theme
- By default, Android 10+ supports system-wide dark theme.
- To support older versions, use `AppCompatDelegate`:

```kotlin
AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_FOLLOW_SYSTEM)
```

---

## For Jetpack Compose Apps

### 1. Define Light and Dark Color Schemes
- Use `lightColors` and `darkColors` to define color palettes.

```kotlin
private val LightColors = lightColors(
    primary = Color(0xFF6200EE),
    // ...existing code...
)
private val DarkColors = darkColors(
    primary = Color(0xFFBB86FC),
    // ...existing code...
)
```

### 2. Apply Theme Based on System Setting

```kotlin
@Composable
fun MyAppTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    val colors = if (darkTheme) DarkColors else LightColors
    MaterialTheme(
        colors = colors,
        // ...existing code...
        content = content
    )
}
```

### 3. Use Theme in Your App

```kotlin
@Composable
fun MyApp() {
    MyAppTheme {
        // ...existing code...
    }
}
```

---

## Testing Dark Theme

- Switch device or emulator to dark mode in system settings.
- Verify your app adapts colors and styles accordingly.

---

## Summary

- Define separate resources for light and dark themes.
- Use theme attributes and system settings to switch themes automatically.
- In Compose, use `isSystemInDarkTheme()` and provide both color palettes.