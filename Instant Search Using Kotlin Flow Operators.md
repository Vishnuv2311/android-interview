# 🔎 Instant Search Using Kotlin Flow Operators  

## 📌 Overview  
Instant search allows users to get **real-time search results** as they type. **Kotlin Flow** provides powerful operators like:  
- ✔ **`debounce()`** – Waits for a pause before processing input to reduce unnecessary API calls.  
- ✔ **`distinctUntilChanged()`** – Prevents duplicate searches for the same query, minimizing processing.  
- ✔ **`flatMapLatest()`** – Cancels old API calls when a new query is entered, ensuring only the latest result is used.  

---

## **1️⃣ How Does Instant Search Work?**  
1️⃣ **User types a query.**  
2️⃣ **`debounce()`** ensures API is called **only after the user stops typing** to avoid frequent API calls.  
3️⃣ **`distinctUntilChanged()`** prevents duplicate API calls for the same query, reducing unnecessary processing.  
4️⃣ **`flatMapLatest()`** cancels previous API calls when a new query is entered, ensuring only the latest result is used.

---

## **2️⃣ Implementing Instant Search with Kotlin Flow**

### **🔹 Step 1: Add Dependencies**
```gradle
dependencies {
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4"  // Coroutines support
    implementation "androidx.lifecycle:lifecycle-runtime-ktx:2.5.0"  // Lifecycle-aware coroutines
}
```
📌 These dependencies enable **Kotlin Flow** and **Lifecycle integration**.

---

### **🔹 Step 2: Define Retrofit API for Search**
```kotlin
import retrofit2.http.GET
import retrofit2.http.Query
import kotlinx.coroutines.flow.Flow

interface ApiService {
    @GET("search")
    fun search(@Query("query") query: String): Flow<List<SearchResult>>
}
```
✅ The API returns a **Flow** that emits search results asynchronously.

---

### **🔹 Step 3: Implement Search Logic in ViewModel**
```kotlin
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.*
import kotlinx.coroutines.launch

class SearchViewModel(private val apiService: ApiService) : ViewModel() {

    private val _searchQuery = MutableStateFlow("")  // Holds the latest query

    val searchResults: StateFlow<List<SearchResult>> = _searchQuery  
        .debounce(300)  // Waits for 300ms before emitting, reducing API calls
        .distinctUntilChanged()  // Prevents duplicate queries
        .flatMapLatest { query ->  
            if (query.isBlank()) {
                flowOf(emptyList())  // If query is empty, return an empty list
            } else {
                apiService.search(query)  // API call
                    .catch { emit(emptyList()) }  // Error handling (e.g., network failures)
            }
        }
        .stateIn(viewModelScope, SharingStarted.Lazily, emptyList())

    fun setSearchQuery(query: String) {
        _searchQuery.value = query  // Updates search query
    }
}
```
✅ **Prevents excessive API calls** and ensures **only the latest query triggers a request**.

---

### **🔹 Step 4: Collect Search Results in UI with RecyclerView**
```kotlin
class MainActivity : AppCompatActivity() {
    private val viewModel: SearchViewModel by viewModels()
    private lateinit var adapter: SearchResultsAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val searchBox: EditText = findViewById(R.id.searchBox)
        val recyclerView: RecyclerView = findViewById(R.id.recyclerView)
        
        adapter = SearchResultsAdapter()
        recyclerView.adapter = adapter

        // Listen to text changes and update ViewModel
        searchBox.addTextChangedListener {
            viewModel.setSearchQuery(it.toString())  // Update search query
        }

        // Collect search results and update RecyclerView
        lifecycleScope.launch {
            viewModel.searchResults.collect { results ->
                adapter.submitList(results)  // Update RecyclerView
            }
        }
    }
}
```
✅ **Ensures real-time UI updates** with an efficient **RecyclerView binding**.

---

### **3️⃣ Key Kotlin Flow Operators Used**
| Operator               | Purpose                                                   |
|------------------------|----------------------------------------------------------|
| `debounce(300)`        | Delays API calls while the user is typing to avoid unnecessary requests. |
| `distinctUntilChanged()` | Prevents duplicate API calls for the same query.        |
| `flatMapLatest()`      | Cancels previous API calls if a new query arrives.      |

---

### **4️⃣ Before vs. After Optimization**
| Approach | Issue | Optimized Solution |
|----------|------|--------------------|
| **Using `Flow` without `debounce()`** | Multiple API calls triggered while typing fast. | Use **`debounce(300)`** to wait until typing stops. |
| **Using `switchMap()` instead of `flatMapLatest()`** | API calls are queued, not canceled. | Use **`flatMapLatest()`** to cancel previous calls. |
| **Not handling errors** | App crashes if API fails. | Use **`catch {}`** to handle failures. |

---

### **5️⃣ Common Pitfalls & Solutions**
| Pitfall | Solution |
|---------|----------|
| **Ignoring `debounce()`** | Leads to excessive API calls, degrading performance. Always debounce to avoid overloading the server. |
| **Not Handling Empty Queries** | Always check if the query is empty before making an API call. |
| **Forgetting to Collect Flow** | Ensure that the Flow is collected inside the UI using `collect` or `stateIn`. |
| **Handling Network Errors Improperly** | Always use `catch {}` to handle API failures gracefully. |

---

## **6️⃣ Performance Optimizations**
- **Use `viewModelScope`** to avoid memory leaks.
- **Apply `stateIn()`** for lifecycle-aware flow collection.
- **Use `diffUtil` in RecyclerView** to optimize UI updates.

---

## **📌 Summary**
✔ **`debounce(300)`**: Prevents API calls while the user is typing.  
✔ **`distinctUntilChanged()`**: Ignores duplicate inputs.  
✔ **`flatMapLatest()`**: Ensures only the latest query triggers an API call.  

✅ **Benefits**:
- **Improves performance** by reducing unnecessary network calls.
- **Enhances user experience** with real-time feedback.
- **Efficient resource usage** by canceling redundant requests.
