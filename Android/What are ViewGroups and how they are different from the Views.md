# What are ViewGroups and how they are different from the Views

## What is a View?
A `View` is the basic building block of UI components in Android. It represents a rectangular area on the screen and is responsible for drawing and event handling. Examples of `View` include `TextView`, `Button`, `ImageView`, etc.

## What is a ViewGroup?
A `ViewGroup` is a special type of `View` that can contain multiple child views. It acts as a container for other views and is responsible for laying them out on the screen. Common `ViewGroup` examples include `LinearLayout`, `RelativeLayout`, `ConstraintLayout`, `FrameLayout`, etc.

## Difference between View and ViewGroup

| Feature       | View  | ViewGroup  |
|--------------|-------|------------|
| Definition  | A basic UI component that draws on the screen | A container that holds multiple child views |
| Purpose | Used to display content (text, images, buttons, etc.) | Used to organize and position multiple views |
| Example | `TextView`, `Button`, `ImageView` | `LinearLayout`, `RelativeLayout`, `ConstraintLayout` |
| Can have children? | No | Yes |
| Event Handling | Directly interacts with user input | Passes user input to child views |

### Example Code
```kotlin
// Example of a View (TextView)
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Hello World" />

// Example of a ViewGroup (LinearLayout with TextView and Button inside it)
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />
</LinearLayout>
```

ViewGroups help in structuring the UI efficiently, while Views are individual UI components that handle user interactions.
