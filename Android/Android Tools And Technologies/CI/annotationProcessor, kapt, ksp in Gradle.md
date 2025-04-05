### annotationProcessor, kapt, ksp in Gradle

In Android and Kotlin development, annotations and code generation tools are often used to reduce boilerplate and improve productivity. Gradle provides different ways to integrate these tools depending on the language and tool being used.

#### 1. annotationProcessor
- **Used with:** Java
- **Purpose:** Enables Java annotation processors (like Dagger, ButterKnife, Room, etc.) to generate code during compilation.
- **Gradle Example:**
  ```groovy
  dependencies {
      implementation 'com.google.dagger:dagger:2.x'
      annotationProcessor 'com.google.dagger:dagger-compiler:2.x'
  }
  ```
- **Note:** Works only with Java sources.

#### 2. kapt (Kotlin Annotation Processing Tool)
- **Used with:** Kotlin
- **Purpose:** Provides support for Java-style annotation processing in Kotlin.
- **Gradle Example:**
  ```kotlin
  plugins {
      id 'org.jetbrains.kotlin.kapt'
  }

  dependencies {
      implementation("com.google.dagger:dagger:2.x")
      kapt("com.google.dagger:dagger-compiler:2.x")
  }
  ```
- **Note:** Slower than KSP as it requires converting Kotlin code to Java stubs.

#### 3. ksp (Kotlin Symbol Processing)
- **Used with:** Kotlin
- **Purpose:** An alternative to kapt, designed specifically for Kotlin to improve performance and better integrate with Kotlin’s language features.
- **Gradle Example:**
  ```kotlin
  plugins {
      id("com.google.devtools.ksp") version "1.9.10-1.0.13"
  }

  dependencies {
      implementation("com.google.dagger:dagger:2.x")
      ksp("com.google.dagger:dagger-compiler:2.x")
  }
  ```
- **Advantages over kapt:**
  - Faster compilation.
  - More Kotlin-friendly.
  - No need to generate Java stubs.

#### When to Use What:
- Use `annotationProcessor` if you're using Java only.
- Use `kapt` if you're using Kotlin but the annotation processor only supports Java.
- Use `ksp` if the annotation processor supports it for better performance in Kotlin projects.
