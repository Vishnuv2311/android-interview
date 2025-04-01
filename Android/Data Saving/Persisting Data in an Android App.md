# Persisting Data in an Android App

Persisting data in an Android app refers to storing data so that it remains available even after the app is closed and reopened. Android provides several options for data persistence:

## 1. SharedPreferences
- Stores key-value pairs.
- Suitable for small amounts of primitive data (e.g., user preferences).
- Usage:
  ```kotlin
  val sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE)
  val editor = sharedPreferences.edit()
  editor.putString("username", "JohnDoe")
  editor.apply()
  ```

## 2. Jetpack DataStore
- Replaces SharedPreferences for better efficiency.
- Supports both Preferences and Proto DataStore.
- Example using Preferences DataStore:
  ```kotlin
  object UserPreferences {
      val Context.dataStore: DataStore&lt;Preferences&gt; by preferencesDataStore(name = "user_prefs")
  }
  ```

## 3. Internal &amp; External Storage
- Internal Storage: Stores private files.
- External Storage: Stores files accessible by other apps (requires permissions).

## 4. SQLite Database
- Structured storage with SQL support.
- Uses Room Library for easier implementation.
- Example using Room:
  ```kotlin
  @Entity
  data class User(
      @PrimaryKey val id: Int,
      val name: String
  )
  ```

## 5. Content Providers
- Shares data between applications.
- Used for managing structured data.

## 6. Cloud Storage &amp; Remote Databases
- Firebase Firestore, Realtime Database, or custom backend APIs.

Choosing the right storage method depends on the data type, size, and app requirements.
