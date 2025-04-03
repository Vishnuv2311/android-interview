# Repository Design Pattern

The Repository Pattern is used to abstract data sources and provide a clean API for data access in an application. It acts as a middle layer between the data layer (such as a database, API, or cache) and the business logic.

## Why Use the Repository Pattern?
- **Decouples Data Sources**: Helps separate data access logic from the rest of the application.
- **Improves Testability**: Makes it easier to write unit tests by allowing mocking of data sources.
- **Centralized Data Access**: Provides a single source of truth for fetching and storing data.

## Implementation in Android
In an Android app, the Repository Pattern is commonly used with ViewModel and LiveData (or Flow in Kotlin).

**Example Implementation:**
```kotlin
class UserRepository(private val apiService: ApiService, private val userDao: UserDao) {
    suspend fun getUser(userId: Int): User {
        val cachedUser = userDao.getUserById(userId)
        return cachedUser ?: apiService.fetchUser(userId).also { userDao.insertUser(it) }
    }
}
```

## Usage in ViewModel:
```kotlin
class UserViewModel(private val userRepository: UserRepository) : ViewModel() {
    private val _user = MutableLiveData<User>()
    val user: LiveData<User> get() = _user

    fun fetchUser(userId: Int) {
        viewModelScope.launch {
            _user.value = userRepository.getUser(userId)
        }
    }
}
```

## Conclusion
The Repository Pattern provides a structured way to handle data, making Android apps more maintainable, scalable, and testable.
