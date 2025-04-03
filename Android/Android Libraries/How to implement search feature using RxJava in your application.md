# How to Implement Search Feature Using RxJava in Your Application

Implementing a search feature using RxJava in an Android application can improve user experience by providing real-time search results with optimized performance.

## Steps to Implement Search Using RxJava

1. **Add RxJava and RxAndroid Dependencies**
   ```gradle
   implementation 'io.reactivex.rxjava3:rxjava:3.x.x'
   implementation 'io.reactivex.rxjava3:rxandroid:3.x.x'
   ```

2. **Set Up Search Observable**
   ```kotlin
   searchEditText.textChanges()
       .debounce(300, TimeUnit.MILLISECONDS) // Add a delay to reduce API calls
       .map { query -> query.toString().trim() }
       .filter { query -> query.length >= 2 } // Prevent unnecessary API calls for short inputs
       .distinctUntilChanged()
       .switchMapSingle { query ->
           searchRepository.search(query)
               .subscribeOn(Schedulers.io())
               .observeOn(AndroidSchedulers.mainThread())
       }
       .subscribe({ results ->
           updateUI(results)
       }, { error ->
           showError(error)
       })
   ```

3. **Breakdown of the Operators Used**
   - `debounce()`: Avoids making API calls for every keystroke.
   - `map()`: Trims input to avoid unnecessary whitespace.
   - `filter()`: Ensures the query is meaningful.
   - `distinctUntilChanged()`: Prevents duplicate queries.
   - `switchMapSingle()`: Cancels previous requests if a new query is entered.
   - `subscribeOn(Schedulers.io())`: Runs the network call on a background thread.
   - `observeOn(AndroidSchedulers.mainThread())`: Updates UI on the main thread.

4. **Implement Repository for API Calls**
   ```kotlin
   class SearchRepository(private val apiService: ApiService) {
       fun search(query: String): Single<List<SearchResult>> {
           return apiService.searchItems(query)
       }
   }
   ```

5. **Handle API Response in ViewModel**
   ```kotlin
   class SearchViewModel(private val repository: SearchRepository) : ViewModel() {
       private val compositeDisposable = CompositeDisposable()

       fun search(query: String) {
           val disposable = repository.search(query)
               .subscribe({ results ->
                   _searchResults.postValue(results)
               }, { error ->
                   _error.postValue(error.message)
               })

           compositeDisposable.add(disposable)
       }

       override fun onCleared() {
           super.onCleared()
           compositeDisposable.clear()
       }
   }
   ```

## Conclusion
Using RxJava for search functionality enhances performance by reducing redundant API calls and handling asynchronous operations efficiently.
