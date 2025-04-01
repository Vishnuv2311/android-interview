# What is Module in Dagger?

In Dagger, a Module is a class annotated with `@Module` that provides dependencies which cannot be directly injected using constructor injection. Modules help supply dependencies that are created outside of your control, such as instances of third-party libraries or objects that require complex initialization.

## Purpose of a Module
- Provides dependencies using `@Provides` annotated methods.
- Helps in injecting interfaces by specifying concrete implementations.
- Can be used to manage dependencies with different scopes.

## Example
```kotlin
@Module
class NetworkModule {

    @Provides
    fun provideOkHttpClient(): OkHttpClient {
        return OkHttpClient.Builder().build()
    }

    @Provides
    fun provideRetrofit(client: OkHttpClient): Retrofit {
        return Retrofit.Builder()
            .baseUrl("https://api.example.com")
            .client(client)
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }
}
```

In this example:
- `provideOkHttpClient` provides an instance of `OkHttpClient`.
- `provideRetrofit` provides an instance of `Retrofit` using the `OkHttpClient`.

## Usage in Component
Modules need to be included in a Dagger Component:
```kotlin
@Component(modules = [NetworkModule::class])
interface AppComponent {
    fun getRetrofit(): Retrofit
}
```

## Summary
- Dagger Modules are used to provide dependencies that cannot be directly injected via constructors.
- They are defined using `@Module` and methods annotated with `@Provides`.
- Modules enhance flexibility and allow better dependency management.
