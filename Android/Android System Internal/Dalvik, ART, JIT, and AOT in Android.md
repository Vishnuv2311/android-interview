# Dalvik, ART, JIT, and AOT in Android

## Dalvik
Dalvik was the original process virtual machine in Android, designed to run applications efficiently on devices with limited resources. It used Just-In-Time (JIT) compilation to translate bytecode into machine code at runtime, which improved execution speed but incurred performance overhead.

## ART (Android Runtime)
ART replaced Dalvik starting from Android 5.0 (Lollipop). Unlike Dalvik, ART primarily uses Ahead-Of-Time (AOT) compilation, meaning that the bytecode is compiled into native machine code during installation, reducing runtime overhead and improving performance. ART also includes Garbage Collection improvements and better memory efficiency.

## Just-In-Time (JIT) Compilation
JIT is a compilation approach where bytecode is converted into native code at runtime. It improves startup time and reduces storage usage but may lead to performance lags due to runtime compilation.

## Ahead-Of-Time (AOT) Compilation
AOT compiles an app’s bytecode into native code before execution, usually at installation. This results in faster execution times and lower CPU usage but requires more storage for precompiled binaries.

## Dalvik vs. ART
| Feature | Dalvik | ART |
|---------|--------|-----|
| Compilation | JIT | AOT (with JIT support in later versions) |
| Performance | Slower due to runtime compilation | Faster due to precompiled code |
| Memory Usage | Higher due to JIT overhead | Lower with optimized GC |
| Battery Efficiency | Less efficient | More efficient |

## JIT + AOT in Modern Android
Recent Android versions use a combination of JIT and AOT for a balance between performance and storage efficiency. The system uses AOT for frequently used code and JIT for optimizing execution dynamically.
