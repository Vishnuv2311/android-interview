# Delegates in Kotlin

Kotlin provides a powerful feature called **delegation**, which allows you to delegate the implementation of properties and behaviors to another object. This helps in achieving code reusability and reducing boilerplate code.

## Types of Delegates in Kotlin

### 1. Property Delegation
Property delegation allows delegating getter and setter logic to another property or function.

Example:
```kotlin
import kotlin.reflect.KProperty

class Delegate {
    operator fun getValue(thisRef: Any?, property: KProperty<*>): String {
        return "Delegated Property"
    }
}

class Example {
    val myProperty: String by Delegate()
}

fun main() {
    val example = Example()
    println(example.myProperty)  // Output: Delegated Property
}
```

### 2. Standard Delegates
Kotlin provides built-in delegates, such as `lazy`, `observable`, and `vetoable`.

- **lazy**: Initializes a property only when it is accessed.
```kotlin
val lazyValue: String by lazy {
    "Computed once"
}
```

- **observable**: Allows listening to property changes.
```kotlin
import kotlin.properties.Delegates

var observedValue: String by Delegates.observable("Initial") { _, old, new ->
    println("Value changed from $old to $new")
}
```

- **vetoable**: Allows controlling property changes.
```kotlin
var vetoValue: Int by Delegates.vetoable(10) { _, old, new ->
    new > old  // Only allow increasing the value
}
```

### 3. Class Delegation
Kotlin supports class delegation using the `by` keyword.

Example:
```kotlin
interface Printer {
    fun printMessage()
}

class SimplePrinter : Printer {
    override fun printMessage() = println("Printing message")
}

class PrinterDelegate(private val printer: Printer) : Printer by printer

fun main() {
    val printer = PrinterDelegate(SimplePrinter())
    printer.printMessage()  // Output: Printing message
}
```

## Advantages of Delegates
- Reduces boilerplate code
- Increases code reusability
- Improves maintainability
- Enhances separation of concerns

Delegates in Kotlin are a great way to simplify code and encourage modular design.
