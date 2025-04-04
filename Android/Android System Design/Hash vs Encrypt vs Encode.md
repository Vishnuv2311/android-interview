# Hash vs Encrypt vs Encode

Understanding the differences between hashing, encryption, and encoding is essential in security and data handling.

## 1. Hashing
- Converts data into a fixed-length string (hash) using a hash function.
- Irreversible: You cannot retrieve the original data from the hash.
- Used for password storage, data integrity checks (e.g., SHA-256, MD5).
- Example:
    ```kotlin
    import java.security.MessageDigest

    fun hashString(input: String, algorithm: String): String {
        return MessageDigest.getInstance(algorithm)
            .digest(input.toByteArray())
            .joinToString("") { "%02x".format(it) }
    }

    fun main() {
        println(hashString("password123", "SHA-256"))
    }
    ```

## 2. Encryption
- Converts data into a secret format using a key, allowing it to be decrypted later.
- Reversible: The original data can be retrieved with the correct key.
- Used for secure communication, storage, and authentication (e.g., AES, RSA).
- Example:
    ```kotlin
    import javax.crypto.Cipher
    import javax.crypto.KeyGenerator
    import javax.crypto.SecretKey

    fun encrypt(data: String, secretKey: SecretKey): ByteArray {
        val cipher = Cipher.getInstance("AES")
        cipher.init(Cipher.ENCRYPT_MODE, secretKey)
        return cipher.doFinal(data.toByteArray())
    }

    fun main() {
        val keyGen = KeyGenerator.getInstance("AES")
        keyGen.init(256)
        val secretKey = keyGen.generateKey()

        val encryptedData = encrypt("Hello, World!", secretKey)
        println(encryptedData.joinToString { it.toString() })
    }
    ```

## 3. Encoding
- Converts data into another format to ensure safe transmission or storage.
- Reversible: No key is required, and it is not meant for security.
- Used in data transmission (e.g., Base64, URL encoding).
- Example:
    ```kotlin
    import java.util.Base64

    fun encodeBase64(data: String): String {
        return Base64.getEncoder().encodeToString(data.toByteArray())
    }

    fun decodeBase64(encoded: String): String {
        return String(Base64.getDecoder().decode(encoded))
    }

    fun main() {
        val encoded = encodeBase64("Hello, World!")
        println(encoded)
        println(decodeBase64(encoded))
    }
    ```

## Summary Table

| Feature       | Hashing           | Encryption       | Encoding         |
|--------------|------------------|-----------------|----------------|
| Purpose      | Data integrity    | Data security   | Data representation |
| Reversible   | No                | Yes (with key)  | Yes            |
| Security Use | Yes               | Yes             | No             |
| Examples     | SHA-256, MD5      | AES, RSA        | Base64, URL Encoding |

Hashing ensures data integrity, encryption secures data, and encoding transforms data for compatibility.
