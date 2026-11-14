# RetroShare Mobile

RetroShare Mobile is a Flutter client for RetroShare that runs on Android, iOS and Windows.

Repository: <https://github.com/RetroShare/retroshare-mobile-v2>

## Get the source

```
git clone https://github.com/RetroShare/retroshare-mobile-v2.git
cd retroshare-mobile-v2
flutter pub get
```

## Prerequisites

- **Flutter SDK**: <https://docs.flutter.dev/get-started/install>
- **Git**: <https://gitforwindows.org/> on Windows
- **Android Studio** with the Android SDK, for Android builds: <https://developer.android.com/studio>
- **Visual Studio 2022** with the *Desktop development with C++* workload, for Windows builds. The Community edition is enough.

Run `flutter doctor` and fix anything it reports for the platform you want to build.

## Build for Android

1. Accept the Android SDK licenses:

        flutter doctor --android-licenses

2. Enable USB debugging on your phone and plug it in, or start an emulator from Android Studio.
3. Check that the device is listed:

        flutter devices

4. Run the app (leave out `--release` for a debug build):

        flutter run --release

## Build for Windows (desktop)

The Windows app needs the RetroShare backend, `retroshare-service.exe`, together with its DLLs (for example `libstdc++-6.dll`, Botan or Qt, depending on how you built it). See [Compilation](compilation.md) for building RetroShare on Windows.

1. Enable Windows desktop support:

        flutter config --enable-windows-desktop

2. If the project has no `windows` folder, generate it:

        flutter create --platforms=windows .

3. Build the frontend:

        flutter run -d windows

    This produces `build\windows\x64\runner\Debug\retroshare-mobile.exe`.

4. Make the backend DLLs available in one of these ways:

    - Add their folder to your user `PATH`, for example `C:\msys64\mingw64\bin` for MSYS2/MinGW builds.
    - Copy the DLLs next to the executables.

5. Copy `retroshare-service.exe` into `build\windows\x64\runner\Debug\`, next to `retroshare-mobile.exe`.
6. Start the app again:

        flutter run -d windows

The app starts `retroshare-service.exe` in the background, connects to it on `127.0.0.1:9092`, and stops it when you close the app.

**"Invalid argument" or "Access Denied" when copying files:** an old `retroshare-mobile.exe` process is still running and has the build files locked. Stop it in PowerShell, then run `flutter run -d windows` again:

```
Stop-Process -Name retroshare-mobile -Force
```

## Debugging on Android

Use `adb` (in the Android SDK `platform-tools` folder) to capture logs:

```
adb logcat > trace.txt
```
To query the service JSON API directly from your PC, forward its port first:

```
adb forward tcp:9091 tcp:9092
curl http://127.0.0.1:9091/RsJsonApi/version
```
