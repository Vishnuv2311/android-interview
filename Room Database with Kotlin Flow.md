# 🗄️ Room Database with Kotlin Flow

## 📌 Overview  
**Room Database** is a **Jetpack component** that provides an **SQLite abstraction** for Android.  
When combined with **Kotlin Flow**, it enables **asynchronous database operations** with **real-time updates**.

### ✅ Benefits of Using Flow with Room
- **Efficient background execution** without blocking UI.  
- **Auto-updating Live Data Streams** when data changes.  
- **Transformation operators** like `map()`, `filter()`.  

---

## **1️⃣ Adding Dependencies**
### 🔹 Step 1: Add Room & Kotlin Flow Dependencies  
Add the required dependencies in your **`build.gradle`** (Module-level):

```gradle
dependencies {
    implementation "androidx.room:room-runtime:2.5.0"
    kapt "androidx.room:room-compiler:2.5.0"
    implementation "androidx.room:room-ktx:2.5.0"  // Enables Flow support

    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4"
}
```

---

## **2️⃣ Define Room Entities**
### 🔹 Step 2: Create a Data Entity
```kotlin
import androidx.room.Entity
import androidx.room.PrimaryKey

@Entity(tableName = "posts")
data class Post(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val title: String,
    val content: String
)
```
📌 Each instance of `Post` represents a row in the `posts` table.

---

## **3️⃣ Define DAO (Data Access Object)**
### 🔹 Step 3: Create DAO Interface
```kotlin
import androidx.room.*
import kotlinx.coroutines.flow.Flow

@Dao
interface PostDao {
    @Insert(onConflict = OnConflictStrategy.REPLACE)
    suspend fun insertPost(post: Post)

    @Query("SELECT * FROM posts ORDER BY id DESC")
    fun getAllPosts(): Flow<List<Post>>  // Returns Flow (auto-updating data stream)

    @Delete
    suspend fun deletePost(post: Post)
}
```
📌 Using `Flow<List<Post>>` ensures that data updates automatically when the database changes.

---

## **4️⃣ Create the Room Database**
### 🔹 Step 4: Define Room Database Class
```kotlin
import androidx.room.Database
import androidx.room.Room
import androidx.room.RoomDatabase
import android.content.Context

@Database(entities = [Post::class], version = 1, exportSchema = false)
abstract class AppDatabase : RoomDatabase() {
    abstract fun postDao(): PostDao

    companion object {
        @Volatile
        private var INSTANCE: AppDatabase? = null

        fun getDatabase(context: Context): AppDatabase {
            return INSTANCE ?: synchronized(this) {
                val instance = Room.databaseBuilder(
                    context.applicationContext,
                    AppDatabase::class.java,
                    "app_database"
                ).build()
                INSTANCE = instance
                instance
            }
        }
    }
}
```
📌 `getDatabase()` ensures only **one instance** of Room Database is created (Singleton Pattern).

---

## **5️⃣ Implement Repository**
### 🔹 Step 5: Create a Repository for Database Operations
```kotlin
class PostRepository(private val postDao: PostDao) {
    val allPosts: Flow<List<Post>> = postDao.getAllPosts()  // Exposing Flow

    suspend fun insertPost(post: Post) {
        postDao.insertPost(post)
    }

    suspend fun deletePost(post: Post) {
        postDao.deletePost(post)
    }
}
```
📌 Repository handles data operations and **provides Flow for UI updates**.

---

## **6️⃣ Implement ViewModel**
### 🔹 Step 6: Create ViewModel to Handle UI Data
```kotlin
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.launch

class PostViewModel(private val repository: PostRepository) : ViewModel() {
    val posts = repository.allPosts  // Live Flow of Posts

    fun addPost(title: String, content: String) {
        viewModelScope.launch {
            repository.insertPost(Post(title = title, content = content))
        }
    }

    fun deletePost(post: Post) {
        viewModelScope.launch {
            repository.deletePost(post)
        }
    }
}
```
📌 `viewModelScope.launch` ensures coroutines are **lifecycle-aware**.

---

## **7️⃣ Collecting Data in Activity/Fragment**
### 🔹 Step 7: Observe Flow from ViewModel
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.activity.viewModels
import androidx.lifecycle.lifecycleScope
import kotlinx.coroutines.launch

class MainActivity : AppCompatActivity() {
    private val viewModel: PostViewModel by viewModels()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        lifecycleScope.launch {
            viewModel.posts.collect { posts ->
                println("Updated Posts: $posts")  // Display or update UI
            }
        }
    }
}
```
📌 Using `lifecycleScope.launch`, Flow collection **stops when UI is destroyed**.

---

## **8️⃣ Handling Database Errors with retry()**
If a database query fails, we can retry it before showing an error.
```kotlin
val safePosts: Flow<List<Post>> = repository.allPosts
    .retry(3)  // Retry up to 3 times if an error occurs
    .catch { println("Database Error: ${it.message}") }  // Handle error safely
```
📌 Ensures **resilience against transient failures**.

---

## **9️⃣ Comparing Flow vs LiveData in Room**
| Feature | Flow | LiveData |
|---------|------|---------|
| **Execution** | Works with Coroutines | Works with Lifecycle |
| **Thread Blocking** | Non-blocking | Non-blocking |
| **Supports Operators (`map`, `filter`)** | ✅ Yes | ❌ No |
| **Auto Updates with DB Changes** | ✅ Yes | ✅ Yes |
| **Can be Collected Outside UI** | ✅ Yes | ❌ No |

---

## **📌 Summary**
✅ **Use Room with Kotlin Flow** for automatic database updates.  
✅ **Exposing `Flow<List<Post>>`** allows real-time UI updates.  
✅ **Use `viewModelScope.launch`** for lifecycle-aware DB operations.  
✅ **Use `retry()` and `catch()`** for error handling.  
