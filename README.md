# ASK Online for Android

An Android WebView shell for `https://new.ask-online.net/dashboard`.

## Included behavior

- ASK Online pages stay inside the app.
- External links open in the appropriate Android app/browser.
- JavaScript, DOM storage, cookies, and third-party cookies support the existing login flow.
- File uploads use Android's system picker.
- Downloads go to the public Downloads directory and keep the authenticated cookie.
- Android's Back button navigates web history before closing the app.
- HTTPS-only network policy and Safe Browsing are enabled.
- A retry screen appears when the dashboard cannot load.

No ASK Online password or session is embedded in the app.

## Build a debug APK

### Without installing Android Studio (GitHub cloud build)

1. Create an empty GitHub repository.
2. Upload the **contents** of this project folder to the repository root. Ensure
   `.github/workflows/build-apk.yml` is included; using Git from a computer is
   the safest way to retain the `.github` folder.
3. Open the repository's **Actions** tab and select **Build Android APK**.
4. Choose **Run workflow**, wait for the green check, then open the completed run.
5. Under **Artifacts**, download **ASK-Online-debug-APK** and unzip it.
6. Transfer `app-debug.apk` to the Android phone and install it. Android may ask
   you to allow installs from the browser or file manager used to open it.

Each push to the `main` branch also rebuilds the APK automatically. The cloud
build workflow uses Java 17, Gradle 8.9, and the Android build tools supplied on
GitHub's runner.

### With Android Studio

1. Open this folder in Android Studio.
2. Allow Gradle sync to complete (JDK 17).
3. Select **Build > Build APK(s)**.
4. Find the APK at `app/build/outputs/apk/debug/app-debug.apk`.

Or, after generating/adding the Gradle wrapper:

```bash
./gradlew assembleDebug
```

## Before publishing

- Replace the temporary `A` launcher icon with branding you are authorized to use.
- Change `applicationId` if you own a preferred package namespace.
- Test login, CAPTCHA/Turnstile, file upload, downloads, and logout on a physical phone.
- Create and protect a release signing key; never commit it to source control.
- Confirm ASK Online's terms permit distribution of a wrapper app.

## Main configuration

The start URL, allowed host, navigation, downloads, and file picker are in:

`app/src/main/java/com/bigyan/askonline/MainActivity.java`
