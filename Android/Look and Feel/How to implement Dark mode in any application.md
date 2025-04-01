# How to Implement Dark Mode in Any Application

Dark mode is a popular UI feature that reduces eye strain and saves battery life. Below are the steps to implement dark mode in an Android application.

## 1. Define Dark and Light Themes
In your `res/values/themes.xml` (for light mode):
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <style name="Theme.MyApp" parent="Theme.MaterialComponents.DayNight">
        <!-- Light theme colors -->
    </style>
</resources>
```
And in `res/values-night/themes.xml` (for dark mode):
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <style name="Theme.MyApp" parent="Theme.MaterialComponents.DayNight">
        <!-- Dark theme colors -->
    </style>
</resources>
```

## 2. Enable Dark Mode in AndroidManifest.xml
```xml
<application
    android:theme="@style/Theme.MyApp"
    ... >
</application>
```

## 3. Allow Users to Toggle Dark Mode
Use `AppCompatDelegate` to manually switch themes.
```kotlin
fun setDarkMode(enabled: Boolean) {
    val mode = if (enabled) AppCompatDelegate.MODE_NIGHT_YES else AppCompatDelegate.MODE_NIGHT_NO
    AppCompatDelegate.setDefaultNightMode(mode)
}
```

## 4. Persist User Preference
Save the mode preference in `SharedPreferences`:
```kotlin
val sharedPref = getSharedPreferences("Settings", Context.MODE_PRIVATE)
sharedPref.edit().putBoolean("dark_mode", true).apply()
```

## 5. Automatically Adapt to System Setting
Use `AppCompatDelegate.MODE_NIGHT_FOLLOW_SYSTEM` to match the system's dark mode setting.

## 6. Testing Dark Mode
- Enable dark mode in device settings.
- Use Android Studio's "Force Dark Mode" option.

This ensures a consistent and smooth dark mode experience across your application.
