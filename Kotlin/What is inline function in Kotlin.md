# ⚡ Inline Functions in Kotlin  

## 📌 Overview  
An **inline function** in Kotlin is a function that gets **copied (inlined) at the call site** during **compilation**, eliminating function call overhead.  

### ✅ Why Use Inline Functions?  
✔ **Improves performance** by reducing function call overhead.  
✔ **Allows lambda expressions to be inlined**.  
✔ **Reduces memory allocations** by avoiding object creation.  

---

## **1️⃣ How to Define an Inline Function?**  
```kotlin
inline fun logMessage(message: String) {
    println("Log: $message")
}

fun main() {
    logMessage("Hello, Kotlin!")  // This function will be inlined
}

📌 At compile time, the function body replaces the function call.

⸻

2️⃣ When to Use Inline Functions?

Use Case	Should Use inline?
Higher-order functions (functions with lambdas)	✅ Yes
Performance optimization	✅ Yes
Recursive functions	❌ No (Not allowed)
Large functions	❌ No (Increases bytecode size)



⸻

3️⃣ Inline Function with Lambda Parameter

inline fun execute(action: () -> Unit) {
    println("Before execution")
    action()  // This lambda is inlined
    println("After execution")
}

fun main() {
    execute { println("Executing Lambda") }
}

✅ Output:

Before execution  
Executing Lambda  
After execution  

📌 Avoids unnecessary object creation for lambda expressions.

⸻

4️⃣ Using noinline to Exclude Specific Lambdas
	•	By default, all lambda parameters in an inline function are inlined.
	•	Use noinline to exclude specific lambdas from being inlined.

inline fun process(data: String, noinline action: () -> Unit) {
    println("Processing: $data")
    action()  // This lambda is NOT inlined
}

📌 Useful when passing lambda to another function.

⸻

5️⃣ Using crossinline in Inline Functions
	•	crossinline prevents non-local returns inside lambdas in inline functions.
	•	Ensures the lambda does not return early from the calling function.

inline fun executeTask(crossinline action: () -> Unit) {
    println("Starting Task")
    action()  // `crossinline` prevents return from here
    println("Task Completed")
}

📌 Use when a lambda is passed to another function inside an inline function.

⸻

6️⃣ inline vs noinline vs crossinline

Keyword	Purpose
inline	Inlines the function and its lambda parameters
noinline	Prevents specific lambda parameters from being inlined
crossinline	Prevents non-local returns in lambdas



⸻

📌 Summary

✅ Use inline for small, frequently called functions to improve performance.
✅ Use noinline when passing a lambda to another function.
✅ Use crossinline when non-local returns should be prevented.
✅ Avoid inline for large functions or recursion to prevent increased bytecode size.