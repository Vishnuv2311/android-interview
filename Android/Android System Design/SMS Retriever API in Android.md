# SMS Retriever API in Android

The SMS Retriever API allows apps to automatically retrieve SMS containing a one-time password (OTP) without requiring SMS read permissions.

## Steps to Implement SMS Retriever API

1. **Add Dependencies**
   ```gradle
   dependencies {
       implementation 'com.google.android.gms:play-services-auth:20.7.0'
   }
   ```

2. **Start SMS Retriever**
   ```kotlin
   val client = SmsRetriever.getClient(this)
   val task = client.startSmsRetriever()
   task.addOnSuccessListener {
       Log.d("SMSRetriever", "Successfully started")
   }.addOnFailureListener {
       Log.e("SMSRetriever", "Failed to start")
   }
   ```

3. **Register a Broadcast Receiver**
   ```kotlin
   class MySMSBroadcastReceiver : BroadcastReceiver() {
       override fun onReceive(context: Context, intent: Intent) {
           if (SmsRetriever.SMS_RETRIEVED_ACTION == intent.action) {
               val extras = intent.extras
               val status = extras?.get(SmsRetriever.EXTRA_STATUS) as? Status
               when (status?.statusCode) {
                   CommonStatusCodes.SUCCESS -> {
                       val message = extras.get(SmsRetriever.EXTRA_SMS_MESSAGE) as String
                       Log.d("SMSRetriever", "Received SMS: $message")
                   }
                   CommonStatusCodes.TIMEOUT -> {
                       Log.e("SMSRetriever", "SMS retrieval timed out")
                   }
               }
           }
       }
   }
   ```

4. **Register Broadcast Receiver in Activity**
   ```kotlin
   val receiver = MySMSBroadcastReceiver()
   val intentFilter = IntentFilter(SmsRetriever.SMS_RETRIEVED_ACTION)
   registerReceiver(receiver, intentFilter)
   ```

5. **Format the SMS Message**
   ```
   <#> Your OTP is 123456
   ABCDEF1234567890
   ```
   - The last line is the app’s unique hash for verification.

## Advantages of SMS Retriever API
- No need for SMS read permission.
- Improved security with automatic OTP extraction.
- Seamless user experience.

## Limitations
- Requires a predefined SMS format.
- May take up to 5 minutes to retrieve the SMS.
