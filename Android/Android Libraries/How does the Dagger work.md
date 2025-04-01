# How Does Dagger Work?

Dagger is a Dependency Injection (DI) framework that helps manage dependencies in Android applications efficiently. It generates code at compile-time, eliminating reflection-based performance overhead.

## Key Components of Dagger

1. **@Module**  
   - Defines how dependencies are provided.
   - Uses `@Provides` methods to supply objects.

2. **@Inject**  
   - Used to request dependencies in constructors, fields, or methods.

3. **@Component**  
   - Acts as a bridge between `@Module` and `@Inject`.
   - Generates code for dependency graph management.

4. **@Singleton**  
   - Ensures a single instance of a dependency is provided.

## How Dagger Works Internally

1. **Dependency Graph Creation**  
   - Dagger generates a dependency graph at compile time.
   - It determines how objects should be instantiated and injected.

2. **Code Generation**  
   - Dagger creates a `DaggerComponent` class with methods to provide dependencies.

3. **Injection at Runtime**  
   - When an object is requested, Dagger resolves dependencies automatically.

## Example Usage

```java
@Module
class AppModule {
    @Provides
    fun provideRepository(): Repository {
        return RepositoryImpl()
    }
}

@Component(modules = [AppModule::class])
interface AppComponent {
    fun inject(activity: MainActivity)
}

class MainActivity : AppCompatActivity() {
    @Inject lateinit var repository: Repository

    override fun onCreate(savedInstanceState: Bundle?) {
        (application as MyApp).appComponent.inject(this)
        super.onCreate(savedInstanceState)
    }
}
```

## Benefits of Using Dagger

- **Performance**: Compile-time DI eliminates runtime overhead.
- **Scalability**: Works well in large applications with complex dependencies.
- **Testability**: Makes unit testing easier by injecting mock dependencies.

Dagger simplifies dependency management, ensuring cleaner and more maintainable code in Android applications.
