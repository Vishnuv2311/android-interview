# What is a Canvas in Android?

In Android, a **Canvas** is an abstraction that provides drawing methods to render graphics on a **Bitmap** or directly on a **View**. It is used for custom drawing in an app.

## Key Features of Canvas:
- Allows drawing of shapes (rectangles, circles, lines, etc.).
- Supports text rendering.
- Enables bitmap manipulation.
- Provides methods for transformations (scaling, translation, rotation).

## Common Canvas Methods:
- `drawLine(startX, startY, stopX, stopY, paint)`
- `drawRect(left, top, right, bottom, paint)`
- `drawCircle(cx, cy, radius, paint)`
- `drawText(text, x, y, paint)`

## Usage Example:
```kotlin
class CustomView(context: Context) : View(context) {
    private val paint = Paint().apply {
        color = Color.RED
        strokeWidth = 5f
    }

    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        canvas.drawLine(50f, 50f, 200f, 200f, paint)
        canvas.drawCircle(300f, 300f, 100f, paint)
    }
}
```

## When to Use Canvas:
- Creating custom views.
- Implementing drawing applications.
- Creating animations or graphics effects.

Canvas is a powerful tool for rendering custom graphics efficiently in Android applications.
