# How to Encrypt Data in Android

Encrypting data in Android is essential for ensuring security, especially for sensitive user data. There are multiple approaches to encrypting data:

## 1. Using Android's Jetpack Security Crypto Library
Google's Jetpack Security library provides easy-to-use encryption utilities.

### Implementation:
Add the dependency:
```kotlin
implementation("androidx.security:security-crypto:1.1.0-alpha06")
```

Encrypt and Decrypt data:
```kotlin
import androidx.security.crypto.EncryptedSharedPreferences
import androidx.security.crypto.MasterKeys
import android.content.Context

fun getEncryptedPreferences(context: Context): SharedPreferences {
    val masterKeyAlias = MasterKeys.getOrCreate(MasterKeys.AES256_GCM_SPEC)
    
    return EncryptedSharedPreferences.create(
        "secure_prefs",
        masterKeyAlias,
        context,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )
}
```

## 2. Using AES for File Encryption
AES (Advanced Encryption Standard) is a widely used encryption technique.

Example implementation:
```kotlin
import javax.crypto.Cipher
import javax.crypto.KeyGenerator
import javax.crypto.SecretKey
import javax.crypto.spec.IvParameterSpec

fun generateAESKey(): SecretKey {
    val keyGenerator = KeyGenerator.getInstance("AES")
    keyGenerator.init(256)
    return keyGenerator.generateKey()
}

fun encryptData(data: ByteArray, secretKey: SecretKey): Pair<ByteArray, ByteArray> {
    val cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")
    cipher.init(Cipher.ENCRYPT_MODE, secretKey)
    return Pair(cipher.iv, cipher.doFinal(data))
}

fun decryptData(encryptedData: ByteArray, iv: ByteArray, secretKey: SecretKey): ByteArray {
    val cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")
    cipher.init(Cipher.DECRYPT_MODE, secretKey, IvParameterSpec(iv))
    return cipher.doFinal(encryptedData)
}
```

## 3. Using BiometricPrompt for Authentication
Android provides a secure way to encrypt data using biometric authentication.

```kotlin
import androidx.biometric.BiometricPrompt
import androidx.core.content.ContextCompat
import android.app.Activity

fun showBiometricPrompt(activity: Activity) {
    val executor = ContextCompat.getMainExecutor(activity)
    val biometricPrompt = BiometricPrompt(activity, executor,
        object : BiometricPrompt.AuthenticationCallback() {
            override fun onAuthenticationSucceeded(result: BiometricPrompt.AuthenticationResult) {
                // Proceed with encryption or decryption
            }
        })

    val promptInfo = BiometricPrompt.PromptInfo.Builder()
        .setTitle("Biometric Authentication")
        .setNegativeButtonText("Cancel")
        .build()

    biometricPrompt.authenticate(promptInfo)
}
```

## Conclusion
Depending on your use case, you can choose Jetpack Security, AES encryption, or biometric authentication to secure data in Android applications.
