# Adapter Design Pattern

The Adapter Pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces by converting the interface of one class into another that a client expects.

## Use Case in Android
The Adapter Pattern is commonly used in Android development, especially for handling data sets in UI components like RecyclerView, ListView, and Spinner.

## Example Implementation in Android

```kotlin
// Target Interface
interface MediaPlayer {
    fun play(audioType: String, fileName: String)
}

// Adaptee
class AdvancedMediaPlayer {
    fun playMp4(fileName: String) {
        println("Playing MP4 file: $fileName")
    }

    fun playVlc(fileName: String) {
        println("Playing VLC file: $fileName")
    }
}

// Adapter Class
class MediaAdapter : MediaPlayer {
    private val advancedMediaPlayer = AdvancedMediaPlayer()

    override fun play(audioType: String, fileName: String) {
        when (audioType.lowercase()) {
            "mp4" -> advancedMediaPlayer.playMp4(fileName)
            "vlc" -> advancedMediaPlayer.playVlc(fileName)
            else -> println("Invalid media format")
        }
    }
}

// Client Code
fun main() {
    val player: MediaPlayer = MediaAdapter()
    player.play("mp4", "song.mp4")
    player.play("vlc", "movie.vlc")
}
```

## Benefits
- Allows compatibility between different interfaces.
- Promotes reusability of existing code.
- Provides flexibility in integrating different systems.

## Common Use Cases in Android
- `RecyclerView.Adapter` for handling data in lists.
- `ArrayAdapter` for `ListView` and `Spinner`.
- `CursorAdapter` for displaying database queries in a UI component.
