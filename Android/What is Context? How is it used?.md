# What is Context? How is it used?

In Android, `Context` is an abstract class that provides access to application-specific resources and information. It is essential for interacting with system services and accessing components such as databases, preferences, and resources.

## Uses of Context:
1. **Accessing Resources** - Retrieve strings, dimensions, drawables, etc., using `context.getResources()`.
2. **Interacting with System Services** - Obtain system services like `LocationManager`, `ConnectivityManager`, etc., using `context.getSystemService()`.
3. **Starting Activities and Services** - Used to start new activities (`startActivity(Intent)`) and services (`startService(Intent)`).
4. **Broadcasting Intents** - Can send and receive broadcasts via `sendBroadcast(Intent)`.
5. **Accessing Internal Storage and Databases** - Helps in working with shared preferences and databases.

## Types of Context:
- **Application Context (`getApplicationContext()`)**: Associated with the application lifecycle; recommended for operations that need global persistence.
- **Activity Context (`this` in an Activity)**: Tied to an Activity’s lifecycle; used for UI-related operations.
- **Service Context (`this` in a Service)**: Used inside a service to perform background tasks.
- **Base Context (`getBaseContext()`)**: The base context for a context wrapper.

## Best Practices:
- Avoid memory leaks by not holding long-lived references to Activity Context.
- Prefer Application Context for objects with a longer lifecycle than an Activity.
