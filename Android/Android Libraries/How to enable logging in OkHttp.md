# How to enable logging in OkHttp

OkHttp provides a `HttpLoggingInterceptor` that allows you to log request and response details.

## Steps to Enable Logging in OkHttp

1. Add the dependency in your `build.gradle` (if not already added):
   ```gradle
   implementation 'com.squareup.okhttp3:logging-interceptor:4.9.3'
   ```

2. Create an instance of `HttpLoggingInterceptor` and set the desired log level:
   ```java
   import okhttp3.OkHttpClient;
   import okhttp3.logging.HttpLoggingInterceptor;

   HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor();
   loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);

   OkHttpClient client = new OkHttpClient.Builder()
       .addInterceptor(loggingInterceptor)
       .build();
   ```

## Log Levels
The `HttpLoggingInterceptor.Level` has four levels:
- `NONE` – No logs.
- `BASIC` – Logs request and response lines.
- `HEADERS` – Logs request and response headers.
- `BODY` – Logs request and response body.

## Example Output
```plaintext
--> POST https://example.com/api/login
Content-Type: application/json
Content-Length: 50

{"username":"user","password":"password"}

<-- 200 OK (123ms)
Content-Type: application/json
Content-Length: 200

{"token":"abc123","expires_in":3600}
```

This helps in debugging network requests effectively.
