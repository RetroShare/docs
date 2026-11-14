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

## How it works

- When the app starts it requests notification permission and starts the RetroShare service.
- The WebView first shows a login page, then loads RSNewWebUI.
- The core's JSON API listens on `127.0.0.1:9092`, and the WebUI files are served on `127.0.0.1:9090`.
