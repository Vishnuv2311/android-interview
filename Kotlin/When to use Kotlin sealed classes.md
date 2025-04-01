# When to Use Kotlin Sealed Classes

Kotlin's sealed classes are a powerful feature used to represent restricted class hierarchies. They are particularly useful in the following scenarios:

## 1. **Representing Restricted Hierarchies**
   - Sealed classes allow defining a fixed set of subclasses.
   - They ensure that only specific types extend a base class.

## 2. **Handling State and Events in UI Logic**
   - Commonly used in architectures like **MVI (Model-View-Intent)** or **MVVM**.
   - Useful for representing UI states such as **Loading, Success, Error, and Empty**.

   ```kotlin
   sealed class UiState {
       object Loading : UiState()
       data class Success(val data: String) : UiState()
       data class Error(val message: String) : UiState()
   }
   ```

## 3. **When Using Exhaustive `when` Expressions**
   - The compiler ensures all subclasses are covered, eliminating the need for an `else` clause.
   
   ```kotlin
   fun handleState(state: UiState) {
       when (state) {
           is UiState.Loading -> println("Loading...")
           is UiState.Success -> println("Data: ${state.data}")
           is UiState.Error -> println("Error: ${state.message}")
       }
   }
   ```

## 4. **Network and API Response Handling**
   - Sealed classes can help manage network responses effectively.

   ```kotlin
   sealed class NetworkResult<out T> {
       data class Success<T>(val data: T) : NetworkResult<T>()
       data class Failure(val error: String) : NetworkResult<Nothing>()
   }
   ```

## 5. **Representing Intentions in User Actions**
   - Helps model user interactions in a type-safe manner.

   ```kotlin
   sealed class UserAction {
       object Click : UserAction()
       object Swipe : UserAction()
       data class Type(val input: String) : UserAction()
   }
   ```

## Conclusion
Sealed classes provide a structured way to model data states and events in Kotlin applications. They ensure type safety, maintainability, and better control over class hierarchies.
