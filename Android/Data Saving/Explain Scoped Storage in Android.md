# Scoped Storage in Android

Scoped Storage is a security and privacy feature introduced in Android 10 (API level 29) to restrict direct access to shared storage and enhance user data protection.

## Key Features of Scoped Storage:
1. **Limited Direct File Access**  
   - Apps can no longer access arbitrary files in external storage without user permission.
   - Access is granted via MediaStore APIs or the Storage Access Framework (SAF).

2. **Private App Storage**  
   - Apps can read and write freely to their own app-specific storage (`/Android/data/` and `/Android/obb/`).

3. **Media File Access**  
   - Apps can access media files (images, videos, audio) using MediaStore without requiring `READ_EXTERNAL_STORAGE` permission.

4. **Document and File Access**  
   - For non-media files, apps must use the Storage Access Framework (SAF) to let users choose files.

5. **Batch Operations and Performance Improvements**  
   - Scoped Storage improves performance by reducing the need for global storage scanning.

## How to Implement Scoped Storage:
1. **Access Media Files:**
   ```kotlin
   val projection = arrayOf(MediaStore.Images.Media._ID)
   val cursor = contentResolver.query(
       MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
       projection,
       null,
       null,
       null
   )
   ```

2. **Use App-Specific Storage:**
   ```kotlin
   val file = File(context.getExternalFilesDir(null), "example.txt")
   file.writeText("Hello, Scoped Storage!")
   ```

3. **Request User Access via SAF:**
   ```kotlin
   val intent = Intent(Intent.ACTION_OPEN_DOCUMENT).apply {
       addCategory(Intent.CATEGORY_OPENABLE)
       type = "image/*"
   }
   startActivityForResult(intent, REQUEST_CODE)
   ```

## Exceptions:
- Apps targeting API 28 or lower can request `requestLegacyExternalStorage="true"` in `AndroidManifest.xml` to temporarily bypass Scoped Storage.
- Apps with special use cases (e.g., file managers) can request `MANAGE_EXTERNAL_STORAGE` permission from users.

Scoped Storage improves data security while ensuring a seamless user experience with media access APIs.
