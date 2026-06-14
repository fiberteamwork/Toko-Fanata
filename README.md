# Toko-Fanata

## Android APK CI

This repository includes a GitHub Actions workflow at `.github/workflows/android-build.yml` to build an Android APK.

### What it does

- Checks out the repository
- Sets up JDK 17
- Caches Gradle
- Builds a release APK if signing secrets are configured
- Builds a debug APK when no keystore secret is provided
- Uploads APK files as workflow artifacts

### Required secrets for signed release builds

Add these secrets in GitHub repository Settings > Secrets > Actions:

- `KEYSTORE_BASE64` — base64-encoded `.jks` or `.keystore` file
- `KEYSTORE_PASSWORD` — keystore password
- `KEY_ALIAS` — key alias
- `KEY_PASSWORD` — key password

### Example command to generate `KEYSTORE_BASE64`

```bash
base64 -w 0 release.keystore > keystore.base64.txt
```

Then copy the generated string into the `KEYSTORE_BASE64` secret.

### How to run

Use the GitHub Actions UI or push to `main`.

If no signing secret is set, the workflow will build a debug APK instead.
