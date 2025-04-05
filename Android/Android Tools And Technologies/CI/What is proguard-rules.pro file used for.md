# What is proguard-rules.pro file used for?

The `proguard-rules.pro` file in an Android project is used to customize and configure the behavior of ProGuard or R8, which are tools for code shrinking, obfuscation, and optimization.

## Primary Uses:

1. **Code Shrinking**  
   Removes unused classes, methods, fields, and attributes from your code and libraries, reducing the final APK size.

2. **Obfuscation**  
   Renames classes, methods, and fields to meaningless names to make reverse engineering more difficult.

3. **Optimization**  
   Optimizes bytecode and removes redundant code, improving performance.

4. **Preserving Code**  
   Certain classes (e.g., ones used via reflection) need to be explicitly preserved. `proguard-rules.pro` allows you to specify rules such as:
   ```
   -keep class com.example.MyClass { *; }
   ```

5. **Troubleshooting and Debugging**  
   You can configure ProGuard to keep specific methods or include mapping files to de-obfuscate stack traces.

## Common Rules Examples:

- Keep model classes:
  ```
  -keepclassmembers class * {
      @com.google.gson.annotations.SerializedName <fields>;
  }
  ```

- Keep classes used in reflection:
  ```
  -keep class com.example.** { *; }
  ```

- Prevent obfuscation for Retrofit interfaces:
  ```
  -keep interface com.example.api.** { *; }
  ```

## Summary

The `proguard-rules.pro` file ensures that critical code is retained and properly processed during build time while minimizing and protecting the rest of the application code. It is essential when using libraries or reflection-based logic.
