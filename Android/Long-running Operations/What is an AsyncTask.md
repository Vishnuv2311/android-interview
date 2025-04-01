# What is an AsyncTask in Android?

AsyncTask was a class in Android used for performing background operations and updating the UI without having to manipulate threads and handlers manually. It allowed executing short background operations while keeping the UI thread responsive.

## Features of AsyncTask:
- Runs on a separate worker thread but updates the UI thread.
- Provides methods like `onPreExecute()`, `doInBackground()`, `onProgressUpdate()`, and `onPostExecute()`.
- Meant for short background operations, not long-running tasks.

## Lifecycle of AsyncTask:
1. `onPreExecute()` – Runs on the main thread before the task begins.
2. `doInBackground(Params...)` – Runs in the background on a worker thread.
3. `onProgressUpdate(Progress...)` – Runs on the UI thread to update progress.
4. `onPostExecute(Result)` – Runs on the UI thread after completion.

## Example Usage:
```kotlin
class MyAsyncTask : AsyncTask<Void, Int, String>() {
    override fun onPreExecute() {
        super.onPreExecute()
        // Prepare UI before background task starts
    }

    override fun doInBackground(vararg params: Void?): String {
        for (i in 1..5) {
            Thread.sleep(1000) // Simulating work
            publishProgress(i * 20) // Update progress
        }
        return "Task Completed"
    }

    override fun onProgressUpdate(vararg values: Int?) {
        super.onProgressUpdate(*values)
        // Update UI with progress values
    }

    override fun onPostExecute(result: String?) {
        super.onPostExecute(result)
        // Update UI with the final result
    }
}
```

## Why was AsyncTask Deprecated?
- Could lead to memory leaks due to improper handling.
- Difficult to manage multiple tasks running in parallel.
- Inefficient for long-running background tasks.

## Alternatives:
- **Kotlin Coroutines** – Modern approach for async tasks.
- **WorkManager** – Recommended for long-running and persistent tasks.
- **ExecutorService** – More flexible thread management.

**Conclusion:** AsyncTask is deprecated in Android API level 30 and should be replaced with modern alternatives like Coroutines or WorkManager.
