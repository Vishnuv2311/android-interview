# What are Annotations in Android?

Annotations in Android are a form of metadata that provide additional information to the compiler, tools, or runtime about the code. They do not affect the execution of the code but are used for code analysis, lint checks, and improving performance.

## Commonly Used Annotations in Android:

1. **@Override** - Indicates that a method is overriding a method from a superclass.
2. **@Nullable / @NonNull** - Helps prevent null pointer exceptions by specifying whether a parameter, return value, or field can be null.
3. **@Deprecated** - Marks a method, class, or field as obsolete and warns developers to avoid using it.
4. **@SuppressWarnings** - Suppresses specific compiler warnings.
5. **@Keep** - Prevents code from being removed during ProGuard or R8 optimizations.
6. **@WorkerThread, @UiThread, @MainThread, @BackgroundThread** - Ensures that a method runs on the appropriate thread.
7. **@RequiresPermission** - Ensures that a method is only called if the required permission is granted.

## Custom Annotations:
Developers can create their own annotations using `@interface`. For example:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecutionTime {
}
```

Annotations improve code readability, maintainability, and help detect errors early in the development process.
