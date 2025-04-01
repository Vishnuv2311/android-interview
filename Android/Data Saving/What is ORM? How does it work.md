# What is ORM? How Does It Work?

**ORM (Object-Relational Mapping)** is a programming technique that enables developers to interact with a relational database using object-oriented principles instead of SQL queries. It maps database tables to classes and rows to objects, allowing seamless data manipulation.

## How ORM Works:
1. **Mapping Classes to Tables**: Each class corresponds to a table, and class properties represent table columns.
2. **Automatic SQL Generation**: ORM frameworks generate SQL queries for CRUD operations.
3. **Session Management**: ORM handles database connections and transactions efficiently.
4. **Lazy and Eager Loading**: ORM optimizes data retrieval by controlling how and when related data is fetched.
5. **Abstraction Layer**: Developers work with high-level objects rather than raw SQL.

## Common ORM Frameworks in Android:
- **Room** (Jetpack): Google's recommended ORM for SQLite in Android.
- **Realm**: A mobile database with reactive and real-time capabilities.
- **ObjectBox**: A high-performance, lightweight ORM.
- **GreenDAO**: An open-source ORM for Android.

ORM simplifies database interactions, reduces boilerplate code, and improves maintainability in Android applications.
