# MVVM (Model-View-ViewModel) in Android

MVVM (Model-View-ViewModel) is an architectural pattern that helps in separating concerns in Android applications. It promotes a clean code structure, improves maintainability, and enhances testability.

## 📌 Components of MVVM in Android

### 1. Model (M)  
- Represents the data and business logic of the application.  
- Handles network/database operations and provides data to the `ViewModel`.  
- Example:
  ```kotlin
  data class User(val name: String, val age: Int)

  class UserRepository {
      fun getUser(): User {
          return User("Alice", 25)
      }
  }
  ```

### 2. View (V)  
- The UI layer that displays data to the user.  
- Observes the `ViewModel` and updates UI accordingly.  
- Example:
  ```kotlin
  class MainActivity : AppCompatActivity() {
      private val viewModel: UserViewModel by viewModels()

      override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_main)

          viewModel.user.observe(this) { user ->
              textView.text = user.name
          }

          viewModel.fetchUser()
      }
  }
  ```

### 3. ViewModel (VM)  
- Acts as a bridge between `Model` and `View`.  
- Holds UI-related data and survives configuration changes.  
- Example:
  ```kotlin
  class UserViewModel : ViewModel() {
      private val _user = MutableLiveData<User>()
      val user: LiveData<User> get() = _user

      fun fetchUser() {
          _user.value = UserRepository().getUser()
      }
  }
  ```

## ✅ Advantages of MVVM
- **Separation of Concerns**: Keeps UI, business logic, and data management separate.
- **Better Code Maintainability**: Easy to modify and test.
- **Lifecycle Awareness**: `ViewModel` survives configuration changes.
- **Improved UI Performance**: Reduces direct dependency between UI and data sources.

## 🚀 Summary
MVVM is a widely used architectural pattern in Android that improves app structure by separating concerns, making the app more maintainable and scalable.
