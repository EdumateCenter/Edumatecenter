# EduMate Center Android

Android WebView companion application for the EduMate Center mobile app preview.

This repository contains Android source code and GitHub Actions to build a test APK. Do not publicly distribute the debug APK as a production release.

## Build APK

On GitHub, open **Actions → Build EduMate Android APK → Run workflow**, or push an update to the `main` branch. When the build completes, download the **EduMate-debug-APK** artifact from the workflow run.

The app opens https://edumate-mobile-app-preview.edumatecenter.workers.dev/ and follows approved EduMate pages. Login, external links, uploads, and offline functions require real-device testing. A signed release APK/AAB and privacy/store review are still required for production distribution.
