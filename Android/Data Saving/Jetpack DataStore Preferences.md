# Jetpack DataStore Preferences

Jetpack DataStore is a data storage solution that replaces SharedPreferences. It provides a more efficient and safer way to store key-value pairs using Kotlin Coroutines and Flow.

## Advantages of Jetpack DataStore
- Asynchronous and non-blocking (uses Coroutines)
- Stores data in protobuf or preferences format
- Handles data consistency with Flow
- No strict mode violations as in SharedPreferences

## Using Preferences DataStore
Preferences DataStore is a key-value storage solution similar to SharedPreferences but with better performance.

### Implementation Steps:

1. **Add Dependencies**
   ```kotlin
   dependencies {
       implementation "androidx.datastore:datastore-preferences:1.0.0"
   }
   ```

2. **Create a DataStore Instance**
   ```kotlin
   val Context.dataStore: DataStore<Preferences> by preferencesDataStore(name = "settings")
   ```

3. **Write Data**
   ```kotlin
   suspend fun saveBooleanSetting(context: Context, key: String, value: Boolean) {
       val dataStoreKey = booleanPreferencesKey(key)
       context.dataStore.edit { settings ->
           settings[dataStoreKey] = value
       }
   }
   ```

4. **Read Data**
   ```kotlin
   fun getBooleanSetting(context: Context, key: String): Flow<Boolean> {
       val dataStoreKey = booleanPreferencesKey(key)
       return context.dataStore.data.map { preferences ->
           preferences[dataStoreKey] ?: false
       }
   }
   ```

## Conclusion
Jetpack DataStore is a robust alternative to SharedPreferences, offering safer and more efficient data storage.
