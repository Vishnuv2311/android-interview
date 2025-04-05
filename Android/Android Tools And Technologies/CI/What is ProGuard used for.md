## What is ProGuard Used For?

ProGuard is a code shrinker and obfuscator for Java and Android applications. It is primarily used to:

1. **Reduce APK Size**: ProGuard removes unused classes, fields, methods, and attributes, significantly reducing the size of the APK.

2. **Obfuscation**: It renames classes, methods, and fields with obscure names, making it difficult for reverse engineers to understand the code, thereby enhancing security.

3. **Optimization**: ProGuard optimizes bytecode and removes redundant code to improve the runtime performance of the application.

4. **Pre-verification**: It performs pre-verification of bytecode for faster loading and verification on Java Virtual Machines.

ProGuard is typically integrated into the Android build process and can be configured through rules in a `proguard-rules.pro` file.

> Note: R8 is now the default code shrinker and obfuscator for Android builds, which combines the functionalities of ProGuard and D8.
