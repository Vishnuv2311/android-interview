# Android Push Notification System

Android push notifications allow apps to send messages to users even when the app is not actively running. This is primarily handled by Firebase Cloud Messaging (FCM), which is the recommended push notification service by Google.

## How It Works

1. **App Registration**: The app registers with Firebase Cloud Messaging (FCM) and receives a unique registration token.
2. **Sending a Notification**:
   - The server sends a push notification request to FCM, specifying the target device(s) using the registration token(s).
   - FCM processes the request and delivers the notification to the device.
3. **Receiving the Notification**:
   - If the app is in the foreground, the app receives the notification in `onMessageReceived()` of `FirebaseMessagingService`.
   - If the app is in the background or killed, the notification is handled by the system tray.

## Key Components

- **FirebaseMessagingService**: A service to handle incoming push notifications.
- **FCM Console/API**: Allows sending notifications manually or programmatically.
- **Notification Channel (Android 8.0+)**: Required for managing notification settings per channel.
- **PendingIntent**: Used to specify actions when the user taps the notification.

## Advantages

- Works even when the app is not running.
- Efficient and battery-friendly.
- Supports targeting specific users or groups.

## Common Use Cases

- Chat message alerts.
- Promotional offers.
- Order status updates.
- Breaking news alerts.
