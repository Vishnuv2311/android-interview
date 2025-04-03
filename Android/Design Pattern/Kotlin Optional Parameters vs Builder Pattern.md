

 # Kotlin Optional Parameters vs Builder Pattern
 
 This document compares Kotlin's optional parameters and the Builder pattern, explaining when to use each approach.
 
 ## Kotlin Optional Parameters
 
 Kotlin allows functions and constructors to have optional parameters with default values, making it easy to provide flexible APIs without the need for multiple overloads.
 
 **When to use:**
 - Use optional parameters when the number of parameters is small and the defaults are simple.
 - Ideal for simple configurations where only a few values need to be overridden.
 
 **Example:**
 
 ```kotlin
 data class User(
     val name: String,
     val age: Int = 30,
     val email: String = "example@example.com"
 )
 
 fun main() {
     // Using default parameters
     val user1 = User(name = "John")
     // Overriding one default parameter
     val user2 = User(name = "Jane", age = 25)
     println(user1)
     println(user2)
 }
 ```
 
 ## Builder Pattern
 
 The Builder pattern is a creational design pattern that allows constructing complex objects step by step. It is especially useful when an object has many parameters, some of which are optional, or when the construction process is complex.
 
 **When to use:**
 - Use the Builder pattern when the object has many parameters or when the construction process involves multiple steps.
 - Ideal for complex objects where clarity, immutability, and maintainability are important.
 
 **Example:**
 
 ```kotlin
 class User private constructor(
     val name: String,
     val age: Int,
     val email: String
 ) {
     data class Builder(
         var name: String = "",
         var age: Int = 30,
         var email: String = "example@example.com"
     ) {
         fun name(name: String) = apply { this.name = name }
         fun age(age: Int) = apply { this.age = age }
         fun email(email: String) = apply { this.email = email }
         fun build() = User(name, age, email)
     }
 }
 
 fun main() {
     val user = User.Builder()
         .name("John")
         .age(25)
         .build()
     println(user)
 }
 ```
 
 ## Summary
 
 - **Optional Parameters:** Best for simple cases with few parameters and straightforward defaults.
 - **Builder Pattern:** Best for complex object construction with many parameters or when immutability and clarity are required.