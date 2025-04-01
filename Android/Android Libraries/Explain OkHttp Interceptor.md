# OkHttp Interceptor

An **OkHttp Interceptor** is a powerful mechanism in the OkHttp library that allows developers to intercept and modify HTTP requests and responses globally before they are executed.

## Types of Interceptors

OkHttp provides two types of interceptors:

1. **Application Interceptors**:
   - Added when building the `OkHttpClient` using `addInterceptor()`.
   - Useful for tasks like logging, header modification, or request/response transformation.
   - Called only once per request.

2. **Network Interceptors**:
   - Added using `addNetworkInterceptor()`.
   - Operates between the request reaching the network and the response coming back.
   - Useful for cases like caching and modifying network-level details.

## How to Use an Interceptor

Below is an example of adding a logging interceptor:

```kotlin
val loggingInterceptor = HttpLoggingInterceptor().apply {
    level = HttpLoggingInterceptor.Level.BODY
}

val okHttpClient = OkHttpClient.Builder()
    .addInterceptor(loggingInterceptor)
    .build()
```

## Use Cases of OkHttp Interceptors

- **Logging requests and responses**.
- **Adding or modifying headers** (e.g., adding authentication tokens).
- **Request and response compression**.
- **Retrying failed requests**.
- **Offline caching mechanisms**.

OkHttp Interceptors provide fine-grained control over the network operations, making them essential for handling complex API interactions efficiently.
