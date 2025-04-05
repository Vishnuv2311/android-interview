## Build Variants in Android

In Android, build variants are a powerful feature that allow developers to generate different versions of their app from a single codebase. This is typically useful for creating development, staging, and production versions of an app with different configurations.

### Key Concepts

- **Build Types**: Define how a module is built and packaged. By default, Android includes `debug` and `release` build types.
  - `debug`: Used during development, includes debugging tools and is not minified.
  - `release`: Used for production, typically minified and obfuscated.

- **Product Flavors**: Let you create different versions of your app with different features, resources, or configurations.
  - Example: `free` and `paid` versions of the same app.

- **Build Variants**: Are combinations of build types and product flavors.
  - Example: `freeDebug`, `paidRelease`.

### Usage

Build variants can be configured in the `build.gradle` file of your module:

```groovy
android {
    ...
    buildTypes {
        debug {
            applicationIdSuffix ".debug"
            versionNameSuffix "-debug"
        }
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }

    productFlavors {
        free {
            applicationIdSuffix ".free"
            versionNameSuffix "-free"
        }
        paid {
            applicationIdSuffix ".paid"
            versionNameSuffix "-paid"
        }
    }
}
```

### Benefits

- Simplifies testing by generating debug builds with extra tools and logs.
- Enables customization for different user groups or markets.
- Reduces code duplication through shared modules and configuration.

### Best Practices

- Keep flavor-specific code in separate source sets (e.g., `src/free/java`, `src/paid/java`).
- Use build config fields and resource overrides to manage differences.

Build variants provide a flexible and scalable way to manage multiple versions of an Android app efficiently.
