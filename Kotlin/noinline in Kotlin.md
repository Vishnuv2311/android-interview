# 🔹 `noinline` in Kotlin  

## 📌 Overview  
The **`noinline`** modifier in Kotlin is used inside **inline functions** to **prevent specific lambda parameters from being inlined**. By default, all lambda expressions in an inline function are inlined, but `noinline` allows excluding certain lambdas from this behavior.  

---

## **1️⃣ Why Use `noinline`?**  
✔ **Prevents unnecessary code duplication** when a lambda is large.  
✔ **Allows passing lambda functions as parameters to other functions.**  
✔ **Useful when a lambda needs to be stored in a variable or returned.**  

---

## **2️⃣ How to Use `noinline`?**  
### ✅ **Without `noinline` (All Lambdas Are Inlined)**
```kotlin
inline fun process(action1: () -> Unit, action2: () -> Unit) {
    action1()  // Inlined
    action2()  // Inlined
}

📌 Both lambda functions get inlined at the call site.

⸻

✅ With noinline (Prevents Inlining of Specific Lambda)

inline fun process(action1: () -> Unit, noinline action2: () -> Unit) {
    action1()  // Inlined
    action2()  // Not inlined
}

📌 action2 will be treated as a normal function instead of being inlined.

⸻

3️⃣ Why Is noinline Useful?

🔹 Example: Passing noinline Lambda to Another Function

inline fun process(action1: () -> Unit, noinline action2: () -> Unit) {
    action1()
    anotherFunction(action2)  // ✅ Possible because action2 is not inlined
}

fun anotherFunction(action: () -> Unit) {
    action()
}

📌 If action2 was inlined, passing it as a parameter wouldn’t work.

⸻

4️⃣ When to Use noinline?

Use Case	Should Use noinline?
Lambda needs to be stored in a variable	✅ Yes
Lambda is passed to another function	✅ Yes
Lambda is used multiple times in the same function	✅ Yes
Lambda is small and used only once	❌ No (Inlining is better)



⸻

5️⃣ inline vs noinline vs crossinline

Modifier	Description
inline	Inlines the function and all lambda parameters
noinline	Prevents inlining for specific lambda parameters
crossinline	Prevents return from inside a lambda



⸻

📌 Summary

✅ Use noinline when a lambda should NOT be inlined inside an inline function.
✅ Needed when passing lambdas to other functions.
✅ Reduces unnecessary code duplication for large lambda expressions.
✅ Works only inside inline functions.



