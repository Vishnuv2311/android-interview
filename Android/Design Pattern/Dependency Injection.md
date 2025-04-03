# Dependency Injection Design Pattern

Dependency Injection (DI) is a design pattern used to implement Inversion of Control (IoC) by passing dependencies from the outside rather than creating them inside a class. This helps in making code more modular, testable, and maintainable.

## Benefits of Dependency Injection
- **Reduces coupling**: Classes do not depend directly on their dependencies.
- **Improves testability**: Dependencies can be easily mocked for unit testing.
- **Enhances maintainability**: Changing dependencies requires less modification to existing code.

## Types of Dependency Injection
1. **Constructor Injection** - Dependencies are provided through a constructor.
2. **Setter Injection** - Dependencies are set via public setter methods.
3. **Interface Injection** - Dependencies are passed via an interface that the client implements.

## Example in Android (Using Dagger-Hilt)
```kotlin
@HiltAndroidApp
class MyApplication : Application()

@Module
@InstallIn(SingletonComponent::class)
object NetworkModule {
    @Provides
    fun provideRetrofit(): Retrofit {
        return Retrofit.Builder()
            .baseUrl("https://api.example.com")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }
}

@AndroidEntryPoint
class MainActivity : AppCompatActivity() {
    @Inject
    lateinit var retrofit: Retrofit

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        // Now retrofit is available for use
    }
}
```
This example demonstrates how Dagger-Hilt provides dependencies such as `Retrofit` automatically, following the Dependency Injection pattern.
