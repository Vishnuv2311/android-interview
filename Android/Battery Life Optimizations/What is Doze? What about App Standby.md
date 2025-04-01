# What is Doze? What about App Standby?

## Doze Mode
Doze mode is an Android power-saving feature introduced in Android 6.0 (Marshmallow) to extend battery life by reducing background activity when the device is idle. It helps conserve power by restricting network access, background processes, and wakelocks for apps when the device is not in use.

### How Doze Works:
1. **Device is unplugged and stationary** - Android detects that the device is not being used.
2. **Gradual Restrictions** - Background operations are paused in stages:
   - **App network access** is restricted.
   - **Jobs, alarms, and syncs** are deferred.
   - **Wake locks** are ignored.
3. **Idle Maintenance Windows** - Short windows allow apps to complete pending background tasks.
4. **Doze Deepens Over Time** - The longer the device remains idle, the more restrictions are applied.

### Exceptions
- High-priority Firebase Cloud Messages (FCM) can wake an app.
- Apps with foreground services or active notifications may have fewer restrictions.

## App Standby
App Standby is a battery optimization feature that limits background activity for apps that the user has not recently interacted with. Introduced in Android 6.0, it ensures that infrequently used apps do not consume system resources unnecessarily.

### How App Standby Works:
- If an app has **not been launched recently**, it is considered idle.
- Background services, network access, and jobs are restricted.
- The system occasionally allows brief execution windows to handle pending tasks.

### Exceptions
- Apps with **foreground services** are exempt.
- **Whitelisted** apps (such as system-critical apps) can continue normal operation.

## Differences Between Doze and App Standby
| Feature | Doze Mode | App Standby |
|---------|----------|-------------|
| Trigger | Device is stationary & idle | App is unused for a period |
| Restrictions | Background activity, network access, jobs, alarms | Background jobs, network access |
| Exemptions | High-priority FCM messages, foreground services | Foreground services, whitelisted apps |

These optimizations help Android devices conserve battery life while ensuring essential app functions are not severely impacted.
