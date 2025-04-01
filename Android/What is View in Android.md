# What is View in Android?

In Android, a **View** is the basic building block of the UI (User Interface). It is a rectangular area on the screen responsible for drawing and event handling.

## Key Points:
- Views are the base class for all UI components such as **TextView, Button, ImageView, EditText, etc.**
- It is responsible for **measuring, layout, drawing**, and **handling user interactions**.
- Views are part of the **View hierarchy**, where each view is a node in the tree.
- Custom views can be created by extending the `View` class.

## Commonly Used Views:
- **TextView** – Displays text.
- **EditText** – Allows user input.
- **Button** – Clickable button.
- **ImageView** – Displays images.
- **RecyclerView** – Displays large data lists efficiently.

## View Lifecycle:
1. **onMeasure()** – Determines the size.
2. **onLayout()** – Assigns positions.
3. **onDraw()** – Renders the UI.
4. **onTouchEvent()** – Handles user interaction.

## Conclusion:
Views are the fundamental UI components in Android, enabling user interaction and rendering content.
