# RetroShare Web

RetroShare Web is an Android app written in Kotlin. It runs the RetroShare C++ core as a foreground service and shows the RetroShare web interface (RSNewWebUI) in a WebView.

Repository: <https://github.com/RetroShare/retroshare-web>

## Prerequisites

- Android Studio with Android SDK 36
- Java 17
- A device running Android 9 (API 28) or newer: an `arm64-v8a` phone or an `x86_64` emulator

## Build and install

1. Get the source:

        git clone https://github.com/RetroShare/retroshare-web.git
        cd retroshare-web

2. Build the web interface and copy it into the app's assets. This script needs PowerShell:

        powershell -ExecutionPolicy Bypass -File .\scripts\sync-webui.ps1

    Use `-WebUiSourceDir` or `-TargetAssetsDir` if your folders are somewhere else.

3. The RetroShare core comes in as a Gradle dependency, set in `app/build.gradle.kts`. To use your own build of the core, put the `.so` files in `app/src/main/jniLibs/<abi>/`.
4. In Android Studio, choose **Open**, select the `retroshare-web` folder and wait for the Gradle sync to finish.
5. Click **Run 'app'** (`Shift + F10`) to build and install it on your device or emulator.

## Build the APK file

**In Android Studio:** choose **Build > Build Bundle(s) / APK(s) > Build APK(s)**. When the build finishes, click **locate** in the notification to open the folder that contains the APK.

**From the command line**, in the `retroshare-web` folder (run step 2 above first):

On Windows:

    gradlew.bat assembleDebug

On Linux or macOS:

    ./gradlew assembleDebug

The APK is written to `app/build/outputs/apk/debug/app-debug.apk`. To install it on a phone connected over USB:

    adb install app/build/outputs/apk/debug/app-debug.apk

For a release build, use `assembleRelease`. The APK is then written to `app/build/outputs/apk/release/`. It has to be signed before Android will install it. You can sign it in Android Studio with **Build > Generate Signed Bundle / APK**.

## How it works

- When the app starts it requests notification permission and starts the RetroShare service.
- The WebView first shows a login page, then loads RSNewWebUI.
- The core's JSON API listens on `127.0.0.1:9092`, and the WebUI files are served on `127.0.0.1:9090`.
