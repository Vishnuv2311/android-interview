# What are Composable Functions?

Composable functions are the building blocks of Jetpack Compose. They are used to define the UI in a declarative way.

## Characteristics of Composable Functions
1. **Annotated with `@Composable`**:
   - The `@Composable` annotation marks a function as composable, allowing it to describe UI elements.
2. **Declarative**:
   - They describe *what* the UI should look like based on the current state.
3. **Reusable**:
   - Composable functions can be combined and reused to build complex UIs.
4. **Stateless or Stateful**:
   - They can be stateless (rely on parameters) or manage their own state using tools like `remember`.

## Example of a Composable Function
```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```
- This function takes a `name` parameter and displays a `Text` composable with a greeting message.

## Combining Composable Functions
Composable functions can call other composable functions to build complex UIs.

### Example:
```kotlin
@Composable
fun GreetingCard(name: String) {
    Column(
        modifier = Modifier.padding(16.dp)
    ) {
        Greeting(name)
        Text("Welcome to Jetpack Compose!")
    }
}
```
- The `GreetingCard` function combines the `Greeting` function with additional UI elements.

## Key Points
- Composable functions are **lightweight** and **efficient**.
- They are **recomposed** automatically when the state they depend on changes.
- They should be **side-effect free**, meaning they should only describe the UI and not perform actions like logging or network calls.

## Summary
Composable functions are the foundation of Jetpack Compose, enabling developers to build UIs in a modular, declarative, and reusable way. By combining composable functions, you can create dynamic and interactive user interfaces.
