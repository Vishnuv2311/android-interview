# Examples of the Observer Pattern Used in Android

The Observer pattern is widely used in Android to enable a reactive programming approach where one component (Observer) reacts to changes in another component (Observable).

## 1. LiveData
**Example:**
```kotlin
val liveData = MutableLiveData<String>()

val observer = Observer<String> { newValue ->
    println("Updated Value: $newValue")
}

liveData.observe(lifecycleOwner, observer)

liveData.value = "Hello, World!"
```

## 2. RxJava Observables
**Example:**
```kotlin
val observable = Observable.just("Item 1", "Item 2", "Item 3")

observable.subscribe { item ->
    println("Received: $item")
}
```

## 3. EventBus (Greenrobot)
**Example:**
```kotlin
// Post event
EventBus.getDefault().post(MyEvent("New Data"))

// Subscribe to event
@Subscribe(threadMode = ThreadMode.MAIN)
fun onEvent(event: MyEvent) {
    println("Event received: ${event.data}")
}
```

## 4. Broadcast Receivers
**Example:**
```kotlin
val receiver = object : BroadcastReceiver() {
    override fun onReceive(context: Context?, intent: Intent?) {
        println("Broadcast received!")
    }
}

val intentFilter = IntentFilter("com.example.CUSTOM_EVENT")
context.registerReceiver(receiver, intentFilter)
```

These examples demonstrate how the Observer pattern is applied in different ways across Android development.
