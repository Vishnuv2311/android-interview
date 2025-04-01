# What is Overdraw in Android?

Overdraw occurs when the system draws the same pixel multiple times within a single frame. This happens when UI elements are layered inefficiently, leading to wasted GPU processing and higher power consumption.

## Causes of Overdraw
- **Nested Views**: Too many overlapping views.
- **Unoptimized Backgrounds**: Multiple background layers unnecessarily stacked.
- **Translucent Elements**: Using transparency inefficiently increases rendering effort.

## Detecting Overdraw
Android provides a developer option called **"Debug GPU Overdraw"**, which highlights areas with excessive overdraw using color coding:
- **Blue**: 1x overdraw (acceptable)
- **Green**: 2x overdraw (moderate)
- **Light Red**: 3x overdraw (high)
- **Dark Red**: 4x or more (severe)

## Reducing Overdraw
- **Flatten View Hierarchy**: Minimize unnecessary nested views.
- **Use `setBackground(null)`**: Avoid redundant backgrounds.
- **Optimize `draw()` Methods**: Reduce redundant drawing operations.
- **Use Hardware Layers**: Render complex views more efficiently.

Overdraw can negatively impact performance and battery life, so optimizing it is crucial for smooth UI rendering.
