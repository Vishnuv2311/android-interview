# What is Cleartext Traffic?

Cleartext traffic refers to network communication that is not encrypted, meaning data is sent in plain text over the network.

## Risks of Cleartext Traffic

- **Security Risk**: Data sent in cleartext can be intercepted and read by attackers (e.g., via man-in-the-middle attacks).
- **Privacy Risk**: Sensitive information (like passwords, tokens, or personal data) can be exposed if transmitted without encryption.

## Cleartext Traffic in Android

- By default, Android 9 (API level 28) and above block cleartext (HTTP) traffic for all apps.
- Only encrypted traffic (HTTPS) is allowed unless explicitly permitted.

## How to Handle Cleartext Traffic

- **Use HTTPS**: Always use HTTPS for network communication to ensure data is encrypted.
- **Network Security Configuration**: If cleartext traffic is required (e.g., for development or specific domains), you can allow it using a network security configuration file.

### Example: Allow Cleartext Traffic for Specific Domains

```xml
<!-- res/xml/network_security_config.xml -->
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">example.com</domain>
    </domain-config>
</network-security-config>
```

```xml
<!-- AndroidManifest.xml -->
<application
    android:networkSecurityConfig="@xml/network_security_config"
    ...existing code... >
    ...existing code...
</application>
```

## Best Practices

- Avoid using cleartext traffic in production apps.
- Only permit cleartext traffic for trusted domains and only if absolutely necessary.
- Regularly audit your app's network traffic to ensure sensitive data is not exposed.

## Summary

Cleartext traffic is unencrypted network communication that poses security and privacy risks. Android encourages the use of HTTPS and restricts cleartext traffic by default to protect user data.