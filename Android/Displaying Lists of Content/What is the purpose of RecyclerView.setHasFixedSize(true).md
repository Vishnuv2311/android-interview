# What is the purpose of RecyclerView.setHasFixedSize(true)?

The `setHasFixedSize(true)` method in `RecyclerView` is used to optimize performance when the size of the `RecyclerView` does not change dynamically.

## Purpose:
- It informs the `RecyclerView` that the layout size will remain constant.
- Prevents unnecessary re-measurements of child views when changes occur in the adapter.
- Improves scrolling performance by avoiding expensive layout recalculations.

## When to Use:
- When items in the `RecyclerView` have fixed dimensions and their size does not change based on content.
- If adding or removing items does not affect the overall layout size of the `RecyclerView`.

## Example Usage:
```kotlin
recyclerView.setHasFixedSize(true)
```

Setting this to `true` helps in cases where performance improvements are needed in lists with static item sizes.
