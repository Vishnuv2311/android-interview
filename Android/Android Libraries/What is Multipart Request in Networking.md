# What is Multipart Request in Networking?

A **Multipart Request** in networking is a way to send multiple pieces of data in a single HTTP request. It is commonly used when uploading files, images, or sending form data along with other parameters.

## How Multipart Requests Work
- The request is formatted using `multipart/form-data` encoding.
- Each part of the request contains a content type, disposition, and data payload.
- The server parses these parts individually.

## Use Cases
- File uploads (images, documents, videos)
- Sending a combination of text and binary data
- API requests requiring multiple data types

## Example Using OkHttp in Android
```kotlin
val requestBody = MultipartBody.Builder()
    .setType(MultipartBody.FORM)
    .addFormDataPart("name", "John Doe")
    .addFormDataPart("profile_picture", "profile.jpg",
        RequestBody.create(MediaType.parse("image/jpeg"), file))
    .build()

val request = Request.Builder()
    .url("https://example.com/upload")
    .post(requestBody)
    .build()
```

## Advantages
- Efficient for uploading multiple files
- Allows sending both text and binary data
- Well-supported in modern networking libraries

## Considerations
- Larger request sizes can affect performance.
- Properly configure server-side handling to process multipart data.
