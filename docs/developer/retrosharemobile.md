# Setup RetroShare Mobile: Flutter & Android Studio Build Environment
## Windows Install (https://flutter.dev/docs/get-started/install/windows)

# Install Directories 

- FlutterDir:       ``C:\Users\your-user-name\Documents\flutter_windows_x.xx.x-stable\flutter``
- AndroidStudioDir: ``C:\Program Files\Android\Android Studio``
- RSMobileDir:      ``C:\Users\your-user-name\Documents\GitHub\retroshare-mobile``
- RSPlatformTools:  ``C:\Users\your-user-name\AppData\Local\Android\Sdk\platform-tools``

# Get RetroShare Mobile

via GitHub Desktop: [GitHub Desktop Download](https://central.github.com/deployments/desktop/desktop/latest/win32)

In GitHub Desktop -> Clone Repository -> URL > ADD URL & Clone

https://github.com/RetroShare/retroshare-mobile.git

# Install Git

1. Download and install Git for windows
   - https://gitforwindows.org/
   - Git path : ``C:\Program Files\Git\cmd\git.exe``
   - Add in Environment Variables of your account, Git to PATH: ``C:\Program Files\Git\cmd``

# Install Flutter 
1. System requirements: https://flutter.dev/docs/get-started/install/windows#system-requirements
2. Download Flutter stable: https://flutter.dev/docs/get-started/install/windows#get-the-flutter-sdk
3. Extract the Zip (example C:\Users\<your-user-name>\Documents\flutter_windows_stable_x.x.x-stable.)
4. Add in environment variables for your account to the PATH-variable of USER context separated by ';' the explicit full path to flutter\bin: 
```
   FlutterDir\bin
```
5. Open your Flutter dir and start flutter_console.bat and type:
```bash
   flutter doctor
```
   - Flutter checks its environment and will most likely tell you, that
   - Android SDK is missing
   - Android Studio is missing
   - It may also query for chrome but this is not needed

# Install Android Studio
1. Install Android Studio for windows: https://developer.android.com/studio
   - follow the default settings and ensure the installation is done to AndroidStudioDir
2. After installation start Android Studio and let it update if it queries for some
3. Press NEXT-buttons until it is no longer shown
4. Press FINISH and follow until finish
5. On Welcome-Page go into plugins and
   - install dart and flutter and let AS restart
6. On Welcome page select projects: More Action/SDK Manager and than Tab SDK-Tools.
   - Ensure alls "Android SDK"* Entries are installed and especially
   - Ensure "Android SDK command line tools" to be installed
7. Close the SDK Dialog
8. If you wish to use simulated mobiles you may later select in "more actions" AVD Manager and create emulated devices as you need.
9. Set Flutter SDK Path & Dart SDK Path in Android Studio
   - File -> Settings -> Languages & Frameworks  -> Flutter -> Set Flutter SDK Path:
   - ``$(FlutterDir)\flutter`` and click on OK
   - File -> Settings -> Languages & Frameworks  -> Dart    -> Set Dart SDK Path:
   - ``$(FlutterDir)\bin\cache\dart-sdk`` and click on OK

# Associate Flutter and Android Studio
1. Tell Flutter where to find Android Studio:
```bash    
   flutter config --android-studio-dir "AndroidStudioDir"
```
2. You must agree to the licenses of the Android SDK platform:
``` 
   flutter doctor --android-licenses
```
   and accept all.

# Final check of Flutter installation
3. In new Console type:
```
   flutter doctor
```
   it should now tell all (but maybe chrome) is OK.

# RetroShare Mobile: Prepare Project
1. Open Flutter Console
2. CD to RetroShare mobile dir and type:
```
   flutter pub get
```
   to update the flutter package dependancies as need in the project.

3. Alternative: open the RSMobileDir in Android Studio

## Prepare your project for use with emulated devices in Android Studio
1. open Android studio over the RetroShare Mobile project
2. Within the opened Android Studio on the left side in the Project-Tab open the path:  
   "retroshare-mobile/android/app/src/main/java/io/GeneratedPluginRegistrant.java"
3. Start "GeneratedPluginRegistrant.java" by dobbleclick on it.
4. On the rightside on top of the opened registrant:  
   If you see a note "Module SDK is not defined",  
   than click the button "Setup SDK" on the right side of this note.
5. In the opened dialog select any android SDK and click OK.
6. Restart Android Studio.

Now your project - this is to do in any new project - is able to define and use emulated phones.

# Activate USB Debug Mode of the mobile
4. in settings type usb in search
5. select usb-debugging
6. activate it
7. Plug the mobile with usb to the pc
8. if this is the frist time a dialog appears to accepts the key
9. check in flutter console if the device is available:
```
    flutter devices
```
   should now list your mobile as available

# Run the apk on mobile
## Install the service apk on the mobile
### a) physical mobile
1. plug in the USB of the phone
2. activate: USB-usage file transfer
3. load the service apk to the mobile and install it

### b) emulated phone (but not only)
1. For your convenience:  
   Add in environment variables for your account to the PATH-variable of USER context separated by ';' the explicit full path to the command_tools: $(RSPlatformTools) where the adb.exe houses which we will need.
2. Open a cmd-console within the directory of your service apk
3. type in cmd:  
   adb install "YOUR_SERVCIE_APK.apk" <return>

## Run the RestroShare Mobile
type in cmd console:  
```
   flutter run --release
```
without release it gets run in debug mode

# Debugging and Tracing
## Debugging RetroShare-Mobile
RS- Mobile is debugable simply with Android-Studio as usual with. Just intuitiv and relative conmfortable.
## Tracing RS-mobile in the context of the android-activities
Open a cmd-console in the directory of the android ../sdk/patform-tools.
There you will find the adb.exe (Android Debug Bridge).
This tool enables you for excample to get the tracefiles from your android-device 
by
```
adb logcat > trace.txt
```
You may filter the content of trace.txt than by "restroshare" to get only the lines of the clinet and the service without other andoris contextual activities.


## Debugging RetroShare-Service-Apk
TBD; actual not knwon how to setup a debug-environment fort it.  
Hints in context: https://gitlab.com/elRepo.io/elRepo.io-android/-/issues/43

## Tracing RetroShare-Service in the context of the android-activities
As above with the adb.exe tool.
If you want manually check the communication interface of the service 
you may use the cUrl tool.
To use it you must redirect establich a redirection of the ports:
```
adb forward tcp:9091 tcp:9092
```
than you should be able to talk to the servcie directly.
for exc. like:
```
curl http://127.0.0.1:9091/RsJsonApi/version -v
```

This would for exc generate an output like:
```
    *   Trying 127.0.0.1...
    * TCP_NODELAY set
    * Connected to 127.0.0.1 (127.0.0.1) port 9091 (#0)
    > GET /RsJsonApi/version HTTP/1.1  
    > Host: 127.0.0.1:9091  
    > User-Agent: curl/7.55.1  
    > Accept: */*  
    >  
    < HTTP/1.1 200 OK  
    < Access-Control-Allow-Headers: Authorization,DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range  
    < Access-Control-Allow-Methods: GET, POST, OPTIONS  
    < Access-Control-Allow-Origin: *  
    < Access-Control-Expose-Headers: Content-Length,Content-Range  
    < Connection: close  
    < Content-Length: 116  
    < Content-Type: application/json  
    <  
    {
        "major": 0,
        "minor": 6,
        "mini": 6,
        "extra": "-38-g25f58bc10",
        "human": "0.6.6-38-g25f58bc10"
    }* Closing connection 0
```
