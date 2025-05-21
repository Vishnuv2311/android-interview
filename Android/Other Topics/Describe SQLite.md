# Describe SQLite

SQLite is a lightweight, open-source, self-contained relational database engine. It is widely used for local data storage in mobile and embedded applications.

## Key Features
- **Serverless**: No separate server process; the database is integrated into the application.
- **Zero Configuration**: No setup or administration required.
- **Cross-Platform**: Runs on various operating systems.
- **Single File Storage**: Entire database is stored in a single file on disk.
- **ACID Compliant**: Supports Atomicity, Consistency, Isolation, and Durability.
- **SQL Support**: Supports most of the SQL-92 standard.

## SQLite in Android
- Android provides built-in support for SQLite databases.
- Used for storing structured data locally on the device.
- Accessed via classes like `SQLiteOpenHelper`, `SQLiteDatabase`, and `Cursor`.

### Example Usage in Android
```kotlin
class MyDatabaseHelper(context: Context) : SQLiteOpenHelper(context, "mydb", null, 1) {
    override fun onCreate(db: SQLiteDatabase) {
        db.execSQL("CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)")
    }
    override fun onUpgrade(db: SQLiteDatabase, oldVersion: Int, newVersion: Int) {
        // Handle schema updates
    }
}
```

## When to Use SQLite
- When you need to store structured, relational data locally.
- For apps that require complex queries, transactions, or persistent storage.

## Alternatives
- Room (an abstraction layer over SQLite in Android)
- SharedPreferences (for key-value pairs)
- File storage (for unstructured data)

## Summary
SQLite is a reliable and efficient solution for local data storage in Android apps, offering full-featured SQL support without the need for a separate server.
