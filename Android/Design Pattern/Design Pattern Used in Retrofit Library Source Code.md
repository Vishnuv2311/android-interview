# Design Patterns Used in Retrofit

Retrofit, a type-safe HTTP client for Android and Java, utilizes several design patterns to provide a flexible and maintainable architecture. Below are some key design patterns used in its implementation:

## 1. Builder Pattern
- Retrofit uses the Builder pattern to construct instances of the `Retrofit` class.
- Example:
  ```java
  Retrofit retrofit = new Retrofit.Builder()
      .baseUrl("https://api.example.com/")
      .addConverterFactory(GsonConverterFactory.create())
      .build();
  ```

## 2. Factory Pattern
- The `Converter.Factory` and `CallAdapter.Factory` classes in Retrofit follow the Factory pattern to provide different implementations for serialization, deserialization, and call handling.

## 3. Proxy Pattern
- Retrofit uses Java's dynamic proxies to create implementations of API interfaces at runtime.

## 4. Adapter Pattern
- Retrofit uses the Adapter pattern to support different return types such as `Call<T>`, `Observable<T>` (RxJava), and `Flow<T>` (Kotlin Coroutines).

## 5. Singleton Pattern
- The `Retrofit` instance is often used as a Singleton to ensure efficient API communication across the application.

## 6. Strategy Pattern
- Retrofit applies the Strategy pattern for defining multiple serialization and deserialization strategies (e.g., Gson, Moshi, or ScalarsConverter).

These design patterns help make Retrofit a robust, extensible, and maintainable networking library for Android development.
