# Gestures and Animations in Jetpack Compose

Jetpack Compose provides powerful tools for handling gestures and creating animations to enhance user interactions.

## Gestures in Jetpack Compose
Gestures allow users to interact with the UI through touch inputs like clicks, drags, and swipes.

### Common Gesture APIs
1. **`clickable`**: Detects click events.
2. **`pointerInput`**: Handles advanced gestures like drag, swipe, or custom gestures.
3. **`detectTapGestures`**: Detects tap, double-tap, and long-press gestures.

### Example:
```kotlin
@Composable
fun GestureExample() {
    Box(
        modifier = Modifier
            .size(100.dp)
            .background(Color.Blue)
            .pointerInput(Unit) {
                detectTapGestures(
                    onTap = { println("Box tapped") },
                    onLongPress = { println("Box long-pressed") }
                )
            }
    )
}
```

## Animations in Jetpack Compose
Animations make UI transitions smooth and visually appealing.

### Common Animation APIs
1. **`animateDpAsState`**: Animates `Dp` values.
2. **`animateColorAsState`**: Animates color transitions.
3. **`updateTransition`**: Manages complex animations with multiple states.
4. **`rememberInfiniteTransition`**: Creates looping animations.

### Example: Simple Animation
```kotlin
@Composable
fun SimpleAnimationExample() {
    var expanded by remember { mutableStateOf(false) }
    val size by animateDpAsState(if (expanded) 200.dp else 100.dp)

    Box(
        modifier = Modifier
            .size(size)
            .background(Color.Red)
            .clickable { expanded = !expanded }
    )
}
```

### Example: Infinite Transition
```kotlin
@Composable
fun InfiniteAnimationExample() {
    val infiniteTransition = rememberInfiniteTransition()
    val color by infiniteTransition.animateColor(
        initialValue = Color.Red,
        targetValue = Color.Blue,
        animationSpec = infiniteRepeatable(
            animation = tween(durationMillis = 1000),
            repeatMode = RepeatMode.Reverse
        )
    )

    Box(
        modifier = Modifier
            .size(100.dp)
            .background(color)
    )
}
```

## Combining Gestures and Animations
You can combine gestures and animations to create interactive and dynamic UIs.

### Example:
```kotlin
@Composable
fun GestureWithAnimationExample() {
    var offsetX by remember { mutableStateOf(0f) }

    Box(
        modifier = Modifier
            .size(100.dp)
            .offset { IntOffset(offsetX.roundToInt(), 0) }
            .background(Color.Green)
            .pointerInput(Unit) {
                detectDragGestures { change, dragAmount ->
                    change.consume()
                    offsetX += dragAmount.x
                }
            }
    )
}
```

## Best Practices
- Use gestures to make the UI interactive and intuitive.
- Use animations to provide feedback and improve user experience.
- Combine gestures and animations thoughtfully to create seamless interactions.
