# How do you handle bitmaps in Android as it takes too much memory?

Bitmaps can consume a large amount of memory, leading to `OutOfMemoryError` issues. To efficiently handle bitmaps in Android, follow these strategies:

## 1. Load Bitmap Efficiently with `inSampleSize`
Use `BitmapFactory.Options` to downscale images while loading them into memory.

```kotlin
fun decodeSampledBitmapFromResource(res: Resources, resId: Int, reqWidth: Int, reqHeight: Int): Bitmap {
    val options = BitmapFactory.Options().apply {
        inJustDecodeBounds = true
        BitmapFactory.decodeResource(res, resId, this)
        inSampleSize = calculateInSampleSize(this, reqWidth, reqHeight)
        inJustDecodeBounds = false
    }
    return BitmapFactory.decodeResource(res, resId, options)
}

fun calculateInSampleSize(options: BitmapFactory.Options, reqWidth: Int, reqHeight: Int): Int {
    val (height: Int, width: Int) = options.outHeight to options.outWidth
    var inSampleSize = 1
    if (height > reqHeight || width > reqWidth) {
        val halfHeight: Int = height / 2
        val halfWidth: Int = width / 2
        while ((halfHeight / inSampleSize) >= reqHeight && (halfWidth / inSampleSize) >= reqWidth) {
            inSampleSize *= 2
        }
    }
    return inSampleSize
}
```

## 2. Use `Glide` or `Picasso` for Image Loading
Instead of manually handling bitmaps, use third-party libraries like Glide or Picasso.

**Using Glide:**
```kotlin
Glide.with(context)
    .load(imageUrl)
    .into(imageView)
```

**Using Picasso:**
```kotlin
Picasso.get()
    .load(imageUrl)
    .into(imageView)
```

## 3. Use `inBitmap` for Bitmap Reuse
Reuse existing bitmap memory to reduce allocations.

```kotlin
val options = BitmapFactory.Options().apply {
    inMutable = true
    inBitmap = existingBitmap // Reuse existing bitmap
}
val bitmap = BitmapFactory.decodeResource(resources, R.drawable.image, options)
```

## 4. Cache Bitmaps
Store and reuse bitmaps using `LruCache` to minimize redundant memory allocation.

```kotlin
val cacheSize = (Runtime.getRuntime().maxMemory() / 1024) / 8
val bitmapCache = object : LruCache<String, Bitmap>(cacheSize.toInt()) {
    override fun sizeOf(key: String, bitmap: Bitmap): Int {
        return bitmap.byteCount / 1024
    }
}
```

## 5. Use Hardware Bitmaps
For modern Android devices, use hardware-accelerated bitmaps.

```kotlin
val bitmap = BitmapFactory.decodeResource(resources, R.drawable.image).copy(Bitmap.Config.HARDWARE, false)
```

## 6. Recycle Unused Bitmaps
```kotlin
bitmap.recycle()
```

## 7. Avoid Loading Large Bitmaps into Memory
Load images efficiently based on the required dimensions.

Using these methods, you can manage bitmap memory efficiently and prevent `OutOfMemoryError` issues.
