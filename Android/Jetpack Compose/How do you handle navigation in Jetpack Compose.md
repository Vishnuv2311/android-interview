# How Do You Handle Navigation in Jetpack Compose?

Jetpack Compose provides a `Navigation` library to handle navigation between composables. It simplifies navigation by using a declarative approach.

## Setting Up Navigation

### 1. Add Dependencies
Include the `Navigation` library in your `build.gradle` file:
```groovy
dependencies {
    implementation "androidx.navigation:navigation-compose:2.5.3"
}
```

---

### 2. Define a NavHost
The `NavHost` is the central component that manages navigation between composables.

#### Example:
```kotlin
@Composable
fun NavigationExample() {
    val navController = rememberNavController()

    NavHost(navController = navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        composable("details") { DetailsScreen() }
    }
}
```

---

### 3. Navigate Between Screens
Use the `NavController` to navigate between destinations.

#### Example:
```kotlin
@Composable
fun HomeScreen(navController: NavController) {
    Column {
        Text("Home Screen")
        Button(onClick = { navController.navigate("details") }) {
            Text("Go to Details")
        }
    }
}

@Composable
fun DetailsScreen() {
    Text("Details Screen")
}
```

---

## Passing Arguments
You can pass arguments between destinations using the `NavController`.

#### Example:
```kotlin
NavHost(navController = navController, startDestination = "home") {
    composable("home") { HomeScreen(navController) }
    composable("details/{itemId}") { backStackEntry ->
        val itemId = backStackEntry.arguments?.getString("itemId")
        DetailsScreen(itemId)
    }
}
```

```kotlin
@Composable
fun HomeScreen(navController: NavController) {
    Button(onClick = { navController.navigate("details/42") }) {
        Text("Go to Details with ID")
    }
}

@Composable
fun DetailsScreen(itemId: String?) {
    Text("Details for item: $itemId")
}
```

---

## Best Practices
- Use `NavController` to manage navigation and avoid manually managing back stacks.
- Keep navigation logic separate from UI logic for better maintainability.
- Use `rememberNavController` to ensure the `NavController` is properly scoped to the composition.

---

## Summary
Navigation in Jetpack Compose is handled using the `Navigation` library, which provides a declarative and flexible way to manage navigation between composables. By using `NavHost`, `NavController`, and argument passing, you can build seamless navigation flows in your app.
