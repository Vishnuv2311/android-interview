# 🌐 Retrofit with Kotlin Flow

## 📌 Overview  
**Retrofit** is a popular **HTTP client** for Android that simplifies network requests. When combined with **Kotlin Flow**, it allows for efficient handling of **asynchronous API calls**.

### Why Use Flow with Retrofit?
✔ **Asynchronous execution** without blocking threads.  
✔ **Error handling** using `retry()`, `catch()`.  
✔ **Transformation operators** like `map()`, `filter()`.  
✔ **Real-time data updates** by collecting emissions.  

---

## **1️⃣ Setting Up Retrofit with Kotlin Flow**
### **🔹 Step 1: Add Dependencies**
```gradle
dependencies {
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4"
}
```

---

### **🔹 Step 2: Define API Interface**
Use `@GET`, `@POST`, etc., and return `Flow<T>`.
```kotlin
import kotlinx.coroutines.flow.Flow
import retrofit2.http.GET

interface ApiService {
    @GET("posts")
    fun getPosts(): Flow<List<Post>>
}
```
📌 **Why use Flow?** Returning `Flow<List<Post>>` instead of `Call<List<Post>>` allows seamless integration with Coroutines.

---

### **🔹 Step 3: Create Retrofit Instance**
```kotlin
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

object RetrofitClient {
    private val retrofit = Retrofit.Builder()
        .baseUrl("https://jsonplaceholder.typicode.com/")
        .addConverterFactory(GsonConverterFactory.create())
        .build()

    val apiService: ApiService = retrofit.create(ApiService::class.java)
}
```
📌 **Singleton Pattern** ensures one instance of `ApiService`.

---

## **2️⃣ Calling Retrofit API Using Kotlin Flow**
We collect API responses using Flow in the `Repository` class.

```kotlin
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.catch
import kotlinx.coroutines.flow.flow

class Repository(private val apiService: ApiService) {

    fun fetchPosts(): Flow<List<Post>> = flow {
        val response = apiService.getPosts()  // Make API call
        emit(response)  // Emit the result
    }.catch { e ->
        println("Error: ${e.message}")  // Handle exceptions
    }
}
```
📌 **Error Handling:** `catch()` prevents app crashes due to API failures.

---

## **3️⃣ Using Flow in ViewModel**
We use `viewModelScope.launch` to call the repository.

```kotlin
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.collect
import kotlinx.coroutines.launch

class PostViewModel(private val repository: Repository) : ViewModel() {

    fun getPosts() {
        viewModelScope.launch {
            repository.fetchPosts().collect { posts ->
                println("Received: $posts")
            }
        }
    }
}
```
📌 **Lifecycle-aware execution** ensures proper cancellation of coroutines.

---

## **4️⃣ Handling API Errors with Retry**
Automatically retry failed API calls using `retry()`.

```kotlin
fun fetchPostsWithRetry(): Flow<List<Post>> = flow {
    emit(apiService.getPosts())  // Fetch data
}.retry(3)  // Retry up to 3 times
.catch { e -> println("Final Error: ${e.message}") }
```
📌 **Retries up to 3 times before failing.**

---

## **5️⃣ Transforming API Response Using Flow Operators**
Modify API data using Flow transformations.

🔹 **Example: Using `map()` to Transform Data**
```kotlin
fun fetchModifiedPosts(): Flow<List<String>> = flow {
    emit(apiService.getPosts())
}.map { posts ->  
    posts.map { "Title: ${it.title}" }  // Transform response
}
```
✅ **Processes data before emitting.**

---

## **6️⃣ Using Flow in an Activity**
```kotlin
class MainActivity : AppCompatActivity() {
    private val viewModel: PostViewModel by viewModels()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        lifecycleScope.launch {
            viewModel.getPosts()
        }
    }
}
```
📌 **Safe Collection:** `lifecycleScope.launch` ensures Flow collection stops when Activity is destroyed.

---

## **7️⃣ Comparing Flow vs Call in Retrofit**

| Feature        | Using `Call<T>`  | Using `Flow<T>` |
|---------------|----------------|----------------|
| Execution     | Sync/Async      | Fully Async    |
| Thread Blocking | Can block UI  | Non-blocking  |
| Transformation | Manual         | Supports `map()`, `filter()` |
| Error Handling | Callbacks (`enqueue()`) | `catch()`, `retry()` |
| Real-time Updates | ❌ No | ✅ Yes |

---

## **Best Practices**
✅ Use Flow for **non-blocking** API calls.  
✅ Use `retry()` to handle **API failures gracefully**.  
✅ Use Flow operators (`map()`, `filter()`) for **data transformations**.  
✅ Use `lifecycleScope.launch` to **safely collect** data in UI components.  

---

📌 **Summary**
- **Retrofit + Flow** provides better async API handling.
- **Retries & Error Handling** using `retry()`, `catch()`.
- **Optimized Transformations** with Flow operators.
- **Lifecycle-aware execution** using `viewModelScope.launch`.

🚀 **Using Retrofit with Flow ensures efficient, clean, and reactive API handling!**  
