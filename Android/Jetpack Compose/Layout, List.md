# Layouts and Lists in Jetpack Compose

Jetpack Compose provides powerful tools for building layouts and displaying lists efficiently.

## Layouts in Jetpack Compose
Layouts are used to arrange composables on the screen. Jetpack Compose offers several predefined layout composables.

### Common Layouts
1. **Column**: Arranges children vertically.
2. **Row**: Arranges children horizontally.
3. **Box**: Stacks children on top of each other.
4. **ConstraintLayout**: Provides more complex positioning using constraints.

### Example:
```kotlin
@Composable
fun LayoutExample() {
    Column(
        modifier = Modifier.padding(16.dp)
    ) {
        Text("Item 1")
        Text("Item 2")
        Text("Item 3")
    }
}
```

## Lists in Jetpack Compose
Lists are used to display a scrollable collection of items. Jetpack Compose provides `LazyColumn` and `LazyRow` for efficient list rendering.

### LazyColumn
- Displays a vertical list of items.
- Only renders visible items, improving performance.

#### Example:
```kotlin
@Composable
fun LazyColumnExample() {
    LazyColumn(
        modifier = Modifier.fillMaxSize(),
        contentPadding = PaddingValues(16.dp)
    ) {
        items(100) { index ->
            Text("Item #$index", modifier = Modifier.padding(8.dp))
        }
    }
}
```

### LazyRow
- Displays a horizontal list of items.

#### Example:
```kotlin
@Composable
fun LazyRowExample() {
    LazyRow(
        modifier = Modifier.fillMaxWidth(),
        contentPadding = PaddingValues(16.dp)
    ) {
        items(10) { index ->
            Text("Item #$index", modifier = Modifier.padding(8.dp))
        }
    }
}
```

## Customizing Layouts and Lists
- Use `Modifier` to customize layouts and lists (e.g., padding, spacing, alignment).
- Combine layouts to create complex UI structures.

### Example:
```kotlin
@Composable
fun CombinedLayoutExample() {
    Row(
        modifier = Modifier.fillMaxWidth(),
        horizontalArrangement = Arrangement.SpaceBetween
    ) {
        Text("Start")
        Text("Center")
        Text("End")
    }
}
```

## Best Practices
- Use `LazyColumn` or `LazyRow` for large datasets to optimize performance.
- Combine layouts to achieve the desired structure.
- Use `Modifier` to fine-tune layout behavior and appearance.
