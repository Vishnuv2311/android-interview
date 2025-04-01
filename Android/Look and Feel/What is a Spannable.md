# What is a Spannable?

A `Spannable` in Android is an interface that allows modification of text appearance and behavior in a `SpannableString` or `SpannableStringBuilder`. It enables applying different styles, colors, and other formatting to specific portions of text without affecting the entire string.

## Use Cases
- Highlighting text with different colors
- Making parts of a text bold, italic, or underlined
- Adding clickable links
- Applying custom fonts or background colors to sections of text

## Example Usage
```kotlin
val spannable = SpannableString("Hello, Spannable!")
spannable.setSpan(ForegroundColorSpan(Color.RED), 7, 16, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
textView.text = spannable
```
In the above example, the word "Spannable" is colored red in a `TextView`.

Spannables are particularly useful for creating rich text in Android applications.
