# How to Avoid API Keys from Check-In into VCS

Exposing API keys in version control systems (VCS) like Git can lead to security risks. Here are best practices to prevent accidental check-in of sensitive keys.

## Best Practices

1. **Use Environment Variables**
   - Store API keys in environment variables and access them in your app at runtime.
   - Do not hardcode keys in source files.

2. **Use Local Properties Files**
   - Store keys in files like `local.properties` (for Android) or `.env` files.
   - Add these files to `.gitignore` so they are not tracked by VCS.

   ```gitignore
   # .gitignore
   local.properties
   .env
   ```

3. **Gradle Properties (Android)**
   - Define keys in `local.properties` and reference them in your `build.gradle` file.
   - Example:
     ```properties
     # local.properties (do not check in)
     API_KEY=your_api_key_here
     ```
     ```groovy
     // build.gradle
     def apiKey = project.findProperty("API_KEY") ?: ""
     ```

4. **Secrets Management Tools**
   - Use tools like [git-secret](https://git-secret.io/), [git-crypt](https://github.com/AGWA/git-crypt), or secret managers (AWS Secrets Manager, Google Secret Manager) for managing sensitive data.

5. **Code Reviews and Scanning**
   - Use automated tools (e.g., [GitGuardian](https://www.gitguardian.com/), [truffleHog](https://github.com/trufflesecurity/trufflehog)) to scan for secrets in your codebase.
   - Enforce code review policies to catch accidental key exposure.

## Summary

- Never hardcode API keys in source files.
- Use environment variables, local properties, and `.gitignore` to keep keys out of VCS.
- Use secret management tools and automated scanning for extra protection.
