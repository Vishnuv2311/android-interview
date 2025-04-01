# 🧪 Unit Testing ViewModel with Kotlin Flow and StateFlow  

## 📌 Overview  
Unit testing **ViewModel** in Kotlin using **Flow** and **StateFlow** is essential for ensuring that the business logic operates correctly. This approach allows for asynchronous data handling, providing a more responsive UI. We leverage `TestCoroutineDispatcher` and `runTest()` to effectively control coroutine execution during tests.

### ✅ What You Will Learn:
- ✔ **Testing ViewModel using StateFlow**.  
- ✔ **Using `TestCoroutineDispatcher` for testing coroutines**.  
- ✔ **Using `Turbine` to test Flow emissions**.  

---

## **1️⃣ Dependencies for Testing**
Add the following dependencies to your `build.gradle` (Module-level):  

```gradle
dependencies {
    testImplementation "org.jetbrains.kotlinx:kotlinx-coroutines-test:1.6.4" // For testing coroutines
    testImplementation "junit:junit:4.13.2" // JUnit for unit testing
    testImplementation "app.cash.turbine:turbine:0.9.0" // For testing Flow emissions
}
```

- 📌 `kotlinx-coroutines-test`: This library allows for testing coroutines in a controlled manner.
- 📌 `junit`: A widely-used framework for writing and running tests in Java and Kotlin.
- 📌 `turbine`: A library that simplifies the testing of Flow emissions, making it easier to assert the sequence of emitted values.

---

## **2️⃣ Example ViewModel with StateFlow**

This ViewModel fetches user data from a repository using StateFlow.

```kotlin
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.launch

class UserViewModel(private val repository: UserRepository) : ViewModel() {

    private val _users = MutableStateFlow<List<User>>(emptyList())  // StateFlow to store users
    val users: StateFlow<List<User>> = _users.asStateFlow()

    fun fetchUsers() {
        viewModelScope.launch {
            repository.getUsers()
                .catch { _users.value = emptyList() }  // Handle errors
                .collect { _users.value = it }
        }
    }
}
```

- 📌 **StateFlow** provides a more modern and flexible approach compared to `LiveData`, offering better support for asynchronous data streams and lifecycle awareness.

---

## **3️⃣ Testing ViewModel with StateFlow**

### 🔹 Step 1: Setup Test Coroutine Dispatcher

```kotlin
import kotlinx.coroutines.ExperimentalCoroutinesApi
import kotlinx.coroutines.test.StandardTestDispatcher
import kotlinx.coroutines.test.runTest
import org.junit.Before
import org.junit.Test
import kotlinx.coroutines.flow.flowOf
import kotlinx.coroutines.test.advanceUntilIdle
import kotlinx.coroutines.flow.emptyFlow
import org.junit.Assert.assertEquals

@ExperimentalCoroutinesApi
class UserViewModelTest {

    private lateinit var viewModel: UserViewModel
    private lateinit var repository: FakeUserRepository
    private val testDispatcher = StandardTestDispatcher()  // Controls coroutine execution

    @Before
    fun setup() {
        repository = FakeUserRepository()
        viewModel = UserViewModel(repository)
    }

    @Test
    fun `fetchUsers() should update StateFlow with user list`() = runTest(testDispatcher) {
        // Given a repository that returns a user list
        repository.setUsers(listOf(User(1, "John Doe"), User(2, "Jane Doe")))

        // When fetchUsers is called
        viewModel.fetchUsers()
        advanceUntilIdle()  // Ensure coroutines complete

        // Then the ViewModel's StateFlow should contain users
        assertEquals(2, viewModel.users.value.size)
        assertEquals("John Doe", viewModel.users.value[0].name)
    }

    @Test
    fun `fetchUsers() should return empty list when repository fails`() = runTest(testDispatcher) {
        // Given a repository that emits an error
        repository.setError(true)

        // When fetchUsers is called
        viewModel.fetchUsers()
        advanceUntilIdle()

        // Then users should be empty
        assertEquals(0, viewModel.users.value.size)
    }
}
```

- ✅ `runTest(testDispatcher)`: This ensures that all coroutines run in a controlled test environment.
- ✅ `advanceUntilIdle()`: This function waits until all coroutines finish execution, making the tests reliable.

---

## **4️⃣ Testing Flow Emissions Using Turbine**

Turbine provides a structured way to test Flow emissions step-by-step.

```kotlin
import app.cash.turbine.test

@ExperimentalCoroutinesApi
@Test
fun `fetchUsers() emits correct values`() = runTest {
    repository.setUsers(listOf(User(1, "Alice"), User(2, "Bob")))

    viewModel.fetchUsers()

    viewModel.users.test {
        assertEquals(emptyList<User>(), awaitItem())  // Initial State
        assertEquals(2, awaitItem().size)  // Final State after fetch
        cancelAndIgnoreRemainingEvents()  // Stop collecting
    }
}
```

- ✅ Turbine allows for a more structured approach to testing the sequence of StateFlow updates, making it easier to assert expected behaviors.

---

## **5️⃣ Mocking Repository for Testing**

Since the real repository interacts with a network/database, we use a Fake Repository.

```kotlin
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.flow
import kotlinx.coroutines.flow.emptyFlow

class FakeUserRepository : UserRepository {
    private var users: List<User> = emptyList()
    private var shouldThrowError = false

    fun setUsers(userList: List<User>) {
        users = userList
        shouldThrowError = false
    }

    fun setError(value: Boolean) {
        shouldThrowError = value
    }

    override fun getUsers(): Flow<List<User>> = flow {
        if (shouldThrowError) throw Exception("Network error")
        emit(users)
    }
}
```

- 📌 This Fake Repository simulates different scenarios for testing the ViewModel's behavior, allowing us to handle both successful and erroneous responses effectively.

---

## **6️⃣ Summary of Best Practices**

- **Test Coroutine Execution**: Use `StandardTestDispatcher()` to control coroutine execution.
- **Trigger ViewModel Methods**: Use `viewModelScope.launch {}` in tests to trigger actions.
- **Wait for Async Execution**: Use `advanceUntilIdle()` to ensure all asynchronous operations complete.
- **Verify StateFlow Updates**: Use `assertEquals()` or `Turbine` to verify updates to `StateFlow`.

---

## 📌 Final Thoughts

- ✅ Utilize `StateFlow` in ViewModel to manage UI state effectively.
- ✅ Employ `runTest()` and `advanceUntilIdle()` for accurate coroutine execution during tests.
- ✅ Mock repository methods to simulate various API responses for comprehensive testing.
- ✅ Leverage `Turbine` for detailed testing of Flow emissions, ensuring expected values are emitted in the correct sequence.
