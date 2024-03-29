#Compile Retroshare for Android  

##Introduction  
Compiling an application for Android is not as easy as one would imagine, 
especially one like RetroShare that has a big codebase and is not well 
documented. This document is aimed to empower the reader so she can 
hopefully succeed or at least have a significant help in compiling her 
own RetroShare APK package installable on Android.

##Preparing The Environement

First of all setup your Qt for Android development environment 
following the guide on the [Qt for android web site](http://doc.qt.io/qt-5/androidgs.html).
At this point you should have Android SDK, Android NDK, and Qt for 
Android working fine, and you should be capable of executing on an 
Android emulator or on your Android phone Qt for Android examples.

But RetroShare is not as simple to compile as those examples. In 
particular, the Android NDK precompiled toolchain is limited and doesn't 
support the full C++ specification, and it is missing some part that is 
needed to build RetroShare. The good news is that Android NDK ships all 
the necessary to build a custom toolchain that is suitable to build 
RetroShare. In order to build the toolchain with needed library RetroShare 
provides the **android-prepare-toolchain.sh**  script; before you execute 
it you should define some variables the script cannot determine in an 
easy and reliable manner by itself in your terminal.



```bash
    # The path where Android NDK is installed in your system
    export ANDROID_NDK_PATH="/opt/android-ndk/"

    ## The path where your fresh compiled toolchain will be installed, make sure
    ## the parent exists
    export NDK_TOOLCHAIN_PATH="/home/$(whoami)/Development/android-toolchains/retroshare-android/"

    ## The CPU architecture of the Android device you want to target
    export ANDROID_NDK_ARCH="arm"

    ## The Android API level the Android device you want to target
    export ANDROID_PLATFORM_VER="19"

    ## The number of core that yout host CPU have (just to speed up compilation) set it to 1 if unsure
    export HOST_NUM_CPU=1

    ./android-prepare-toolchain.sh
```

Now is time for the bad news: as of today Qt assumes you use the NDK 
precompiled toolchain and doesn't have an option to use the custom 
toolchain you just generated, so you need to tweak Qt internals a little 
to make usage of the custom toolchain. First of all you need to determine 
your Qt for Android installation path -in my case it is **/opt/Qt5.7.0/** - 
then find the **mkspecs** directory -in my case it 
is **/opt/Qt5.7.0/5.7/android_armv7/mkspecs** - and then modify qmake 
configuration for the android target according to your toolchain, in 
my case I have done it with the following commands (in the same shell 
I used before, to take advantage of the already set variables):

WARNING: This may need a slight modification if you have a different Qt version.

```bash
    export QT_PATH="/opt/Qt5.7.0/"
    export QT_MAJOR_VERSION="5.7"

    cd ${QT_PATH}/${QT_MAJOR_VERSION}/android_armv7/mkspecs
    sudo --preserve-env -s
    cp -r android-g++ android-g++-backup
    cd android-g++
    sed -i "s|^NDK_TOOLCHAIN_PATH =.*|NDK_TOOLCHAIN_PATH = ${NDK_TOOLCHAIN_PATH}|" qmake.conf
```


##Preparing Qt Creator

Now that your environment is set up you should configure Qt Creator for 
Android following the [official guide](http://doc.qt.io/qtcreator/creator-developing-android.html). 
At the end of this step your Qt Creator should recognize the Android compiler 
and the Qt for Android kit. As we use a custom toolchain one more step is needed.

From the top menu click 
_Tools -> Options... -> Build &amp; Run -> Compilers -> Android GCC (arm-4.9) -> Clone_

Now a new compiler (usually named **Clone of Android GCC (arm-4.9)**) 
should have appeared on your compilers list. Select that compiler and 
press the Browse button to look for your custom toolchain compiler. 
You should find it at **$NDK_TOOLCHAIN_PATH/bin/arm-linux-androideabi-gcc**. 
Select it, then press Apply.

Now go to the Kits tab, select **Android for armeabi-v7a (GCC 4.9, Qt 5.7.0)** 
and press the Clone button. A new kit is created (usually named **Clone of 
Android for armeabi-v7a (GCC 4.9, Qt 5.7.0)**). Now select the new kit 
and change the compiler to the one you have just created.

Your Kit is now ready to use. Now you can open RetroShare as a Qt Creator 
project and in the Projects left menu add the newly created kit if not 
already present, so you can select it on the build type selection button down on the left.

Some of RetroShare modules like **retroshare-gui**, **WebUI** and **sqlcipher** 
are not supported yet on Android so to be able to compile RetroShare without 
errors you will have to go to +

_Qt Creator left pane -> Projects -> Build and Run -> Android SOMESTUFF kit -> 
Build Steps -> qmake -> Additional arguments_

and add the following configurations

```cpp
CONFIG+=no_retroshare_gui CONFIG+=no_retroshare_nogui CONFIG+=no_retroshare_plugins CONFIG+=retroshare_android_service CONFIG+=libresapilocalserver CONFIG+=no_libresapihttpserver CONFIG+=no_sqlcipher CONFIG+=retroshare_qml_app
```

WARNING: SQLCipher is not supported yet on RetroShare for Android. 
This poses a major security concern, we are working to fix this ASAP.

WARNING: Some versions of QtCreator try to find the Android SDK in **/opt/android/sdk**. 
A workaround to this is to make a symbolic link there pointing to your 
SDK installation path, like **mkdir -p /opt/android/sdk && ln -s /home/user/android-sdk-linux /opt/android/sdk** 

##Further Readings

- [http://doc.qt.io/qt-5/android-support.html](http://doc.qt.io/qt-5/android-support.html)  
- [https://developer.android.com/ndk/guides/libs.html](https://developer.android.com/ndk/guides/libs.html)  
- [retroshare://forum?name=Compiling%20nogui%20for%20android&id=8fd22bd8f99754461e7ba1ca8a727995&msgid=4e0f92330600bba9cf978f384f4b7b2f2ca64eff](retroshare://forum?name=Compiling%20nogui%20for%20android&id=8fd22bd8f99754461e7ba1ca8a727995&msgid=4e0f92330600bba9cf978f384f4b7b2f2ca64eff)  
- [retroshare://file?name=Android%20Native%20Development%20Kit%20Cookbook.pdf&size=29214468&hash=0123361c1b14366ce36118e82b90faf7c7b1b136](retroshare://file?name=Android%20Native%20Development%20Kit%20Cookbook.pdf&size=29214468&hash=0123361c1b14366ce36118e82b90faf7c7b1b136)  
