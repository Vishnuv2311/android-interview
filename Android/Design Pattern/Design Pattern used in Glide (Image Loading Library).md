# Design Patterns Used in Glide (Image Loading Library)

Glide, a popular image loading and caching library in Android, utilizes multiple design patterns to enhance performance, maintainability, and flexibility. Below are the key design patterns used in Glide:

## 1. Builder Pattern
Glide follows the Builder Pattern to allow fluent and flexible configuration for image loading. 
```java
Glide.with(context)
     .load(url)
     .placeholder(R.drawable.placeholder)
     .error(R.drawable.error)
     .into(imageView);
```
The `RequestBuilder` helps configure the image request fluently.

## 2. Singleton Pattern
Glide implements the Singleton Pattern to ensure a single instance of the `Glide` class manages the image requests and caching.
```java
Glide.get(context);
```
This ensures memory efficiency and avoids redundant instantiations.

## 3. Factory Pattern
Glide uses the Factory Pattern to create various model loaders, decoders, and encoders dynamically. This is useful for handling different image formats.
```java
new GifDecoder.Factory();
```

## 4. Strategy Pattern
The caching strategy in Glide follows the Strategy Pattern, allowing different caching policies like `ALL`, `NONE`, `SOURCE`, and `RESULT`.
```java
RequestOptions requestOptions = new RequestOptions()
     .diskCacheStrategy(DiskCacheStrategy.ALL);
```

## 5. Observer Pattern
Glide uses the Observer Pattern to manage lifecycle-aware requests. When an activity or fragment is destroyed, Glide automatically cancels the ongoing image requests.
```java
Glide.with(fragment)
     .load(url)
     .into(imageView);
```

## 6. Decorator Pattern
Glide employs the Decorator Pattern in its transformation mechanism, allowing dynamic modification of images.
```java
RequestOptions requestOptions = new RequestOptions()
     .transform(new CircleCrop());
Glide.with(context)
     .load(url)
     .apply(requestOptions)
     .into(imageView);
```

These design patterns contribute to Glide's efficiency, modularity, and ease of use.
