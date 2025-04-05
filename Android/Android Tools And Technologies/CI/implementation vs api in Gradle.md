

### implementation vs api in Gradle

In Gradle, both `implementation` and `api` are used to declare dependencies, but they differ in how they expose those dependencies to other modules that depend on the module where these are declared.

#### `implementation`

- When you use `implementation` to declare a dependency, that dependency is only available within the module itself.
- It is **not exposed** to the modules that depend on your module.
- This improves **build performance** by reducing the number of recompilations needed when a dependency changes.
- Ideal for internal use where the dependency is not part of the module's public API.

#### `api`

- When you use `api` to declare a dependency, that dependency is **exposed to consumers** of your module.
- Any module depending on your module will also be able to access this dependency.
- Use `api` only when you want to **expose** classes or functions from the dependency to other modules.

#### Example

```kotlin
dependencies {
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    api 'com.google.code.gson:gson:2.8.6'
}
```

In this case:
- Other modules that depend on this module **cannot** use Retrofit classes directly.
- But they **can** use Gson classes directly because it's declared as `api`.

#### Summary

| Keyword         | Visible to dependent modules | Recompilation required when dependency changes | Use case                        |
|-----------------|------------------------------|--------------------------------------------------|----------------------------------|
| `implementation`| No                           | Less                                             | Internal module dependency       |
| `api`           | Yes                          | More                                             | Shared API or library dependency |