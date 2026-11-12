# EduMate Center — Google Play release checklist

**Package ID:** `com.edumatecenter.mobile` — confirm it is available and that you have not already registered a different package ID in Play Console. Once uploaded, an app's package ID cannot be changed.

**Current code:** `versionCode 2`, `versionName 1.2.0`, `targetSdk 36`. The Android app currently wraps the EduMate mobile preview website and needs device testing, accessibility, login/application testing, and production-domain review before public release.

## 1. Google Play Console
1. Create the EduMate Center app if it does not already exist; use package `com.edumatecenter.mobile`.
2. Complete the Store listing (title, short/full descriptions, 512px store icon, screenshots, feature graphic), app access instructions, age/content rating, ads declaration, and Data safety form.
3. Publish and verify a comprehensive privacy policy URL covering EduMate's actual application, portal, accounts and third-party processing.
4. Set up a testing track. Some newer personal developer accounts require 12 opted-in testers continuously for 14 days before production eligibility.

## 2. Generate and retain YOUR upload key
Do NOT put the keystore or passwords into Git commits, ChatGPT messages, public storage, or screenshots. Generate an upload keystore locally or through a controlled trusted environment; back it up in a secure password manager. Do NOT reuse the debug signing key.

With JDK installed, an example command is:

```bash
keytool -genkeypair -v -keystore edumate-upload-key.jks -alias edumate-upload -keyalg RSA -keysize 3072 -validity 10000
```

Encode the keystore as a single-line base64 string privately. In repository Settings > Secrets and variables > Actions, set:

- `EDUMATE_KEYSTORE_BASE64` — base64-encoded bytes of `edumate-upload-key.jks`
- `EDUMATE_STORE_PASSWORD` — keystore password
- `EDUMATE_KEY_ALIAS` — alias (`edumate-upload` if using command above)
- `EDUMATE_KEY_PASSWORD` — private key password

## 3. Build signed AAB

GitHub Actions > **Build Signed EduMate Play Store AAB** > Run workflow. If any secret is missing, the job refuses to publish an unsigned release artifact. Once successful, download `EduMate-SIGNED-PlayStore-AAB` from Artifacts, unzip it, and upload the `.aab` to the Play Console test release. Enable Play App Signing when prompted.

This workflow **does not automatically publish** to Google Play. It does not hold Play Console access or Play Developer API credentials.

## 4. Release readiness

- Verify Play Console package ID and signing identity before uploading the first bundle.
- Ensure app icon and branding are owned or authorized by EduMate; temporary graduation-cap graphic is not necessarily the official logo.
- Verify source URLs and production reliability, camera/upload/file chooser, external links, authentication, back-navigation, crash-free operation, and privacy/data collection disclosures.
- Android WebView-only apps may receive extra functionality/content review; ensure sufficient mobile experience and rights to content.
- Obtain policy declarations and production access approval; then submit the signed release for Google review.
