# Android Application Components

Android applications consist of four main components:

1. **Activities**  
   - Represents a single screen with a user interface.  
   - Manages user interactions and navigation.  
   - Lifecycle methods include `onCreate()`, `onStart()`, `onResume()`, etc.

2. **Services**  
   - Runs in the background to perform long-running operations.  
   - No UI interaction.  
   - Can be started (`startService()`) or bound (`bindService()`).  
   - Example: Playing music in the background.

3. **Broadcast Receivers**  
   - Handles system-wide broadcast announcements.  
   - Can receive events like battery low, network change, etc.  
   - Implemented using `onReceive()` method.  
   - Example: Receiving SMS or detecting Wi-Fi connection changes.

4. **Content Providers**  
   - Manages shared app data.  
   - Used to read/write data from shared storage (e.g., Contacts, Media files).  
   - Implemented using `ContentProvider` class.  
   - Example: Accessing contacts from other apps.

## Additional Components

- **Intents**: Messaging objects for communication between components.  
- **Fragments**: Modular UI components within an activity.  
- **ViewModel**: Manages UI-related data lifecycle-aware.  

These components work together to build robust Android applications.
