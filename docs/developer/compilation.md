#Compilation

##Compilation on Linux

![Linux tux logo](../img/developer/tux_logo.png "GNU/Linux")

###Install package dependencies:
#### Debian / Ubuntu / Linux Mint
```bash
   sudo apt install git g++ cmake libbz2-dev libjson-c-dev libssl-dev libsqlcipher-dev \
   libupnp-dev doxygen libxss-dev rapidjson-dev libbotan-2-dev libasio-dev
```

To compile with Qt5:
```bash
   sudo apt install qt5-qmake qtmultimedia5-dev libqt5x11extras5-dev
```

To compile with Qt6:
```bash
   sudo apt install qt6-base-dev qt6-multimedia-dev qt6-5compat-dev
```

Additional dependencies for Feedreader plugin:
```bash
   sudo apt install libxml2-dev libxslt1-dev libcurl4-openssl-dev
```

Additional dependencies for Voip plugin:
```bash
   sudo apt install libavcodec-dev libcurl4-openssl-dev \
   libqt5multimedia5-plugins libspeexdsp-dev
```
Autologin:
```bash
   sudo apt install libsecret-1-dev
```

#### openSUSE
```bash
   sudo zypper install gcc-c++ cmake libqt5-qtbase-devel \
   libqt5-qtmultimedia-devel libqt5-qtx11extras-devel libbz2-devel \
   libopenssl-devel libupnp-devel libXss-devel sqlcipher-devel rapidjson-devel
```

To compile with Qt6:
```bash
   sudo zypper install qt6-base-devel qt6-multimedia-devel qt6-qt5compat-devel
```

Additional dependencies for plugins:
```bash
   sudo zypper install ffmpeg-4-libavcodec-devel libcurl-devel libxml2-devel \
   libxslt-devel speex-devel speexdsp-devel
```

#### Arch Linux / Manjaro / EndeavourOS
```bash
   sudo pacman -S base-devel libgnome-keyring cmake qt5-tools qt5-multimedia qt5-x11extras \
   rapidjson libupnp libxslt libxss sqlcipher botan2 bzip2 json-c
```

To compile with Qt6:
```bash
   sudo pacman -S qt6-base qt6-multimedia qt6-5compat
```

#### RedHat/Fedora
```bash
    sudo dnf install mesa-libGL-devel gcc cmake \
    rapidjson-devel libupnp openssl sqlcipher sqlcipher-devel \
    botan2 botan2-devel json-c-devel bzip2-devel asio-devel libsecret libXScrnSaver-devel
```

To compile with Qt5:
```bash
   sudo dnf install qt5-qtbase-devel qt5-qtmultimedia qt5-qtx11extras
```

To compile with Qt6:
```bash
   sudo dnf install qt6-qtbase-devel qt6-qtmultimedia-devel qt6-qt5compat-devel
```

Additional dependencies for Feedreader plugin:
```bash
   sudo dnf install libxml2-devel libxslt-devel libcurl-devel
```

###Checkout the source code
```bash
   cd ~
   git clone https://github.com/RetroShare/RetroShare.git retroshare
```

###Checkout the submodules
```bash
   cd retroshare
   git submodule update --init --remote libbitdht/ libretroshare/ retroshare-webui/
   git submodule update --init --remote supportlibs/librnp supportlibs/rapidjson supportlibs/restbed
```

###Compile
```bash
   qmake CONFIG+=release CONFIG+=rs_jsonapi CONFIG+=rs_webui
   make
```

###Install
```bash
   sudo make install
```

The executable produced will be:  
```bash
 ~/usr/bin/RetroShare  
```

###For packagers

Packagers can use PREFIX and LIB\_DIR to customize the installation paths:
```bash
	qmake PREFIX=/usr LIB_DIR=/usr/lib64 "CONFIG-=debug" "CONFIG+=release"
	make
	make INSTALL_ROOT=${PKGDIR} install
```

### Build infos

Note: If you installed Qt6 you need to use `qmake6` on the command line.

For the `FeedReader` it is required to append the config option `CONFIG+=retroshare_plugins`.
Make sure `plugins/plugins.pro` contains `FeedReader` in the list of plugins to compile. 

Do not mix plugins compiled with Qt5 with those compiled with Qt6. They work only if they are compiled
with the same Qt version as RetroShare.

Voip is outdated and is not compileable on the latest Debian.

For `Autologin` it is required to append the config option `CONFIG+=rs_autologin`.
 
 
###libsqlcipher
If libsqlcipher is not available as a package

You need to place sqlcipher so that the hierarchy is:

         Home
          |
          +--- retroshare
          |
          +--- lib
                |
                +---- sqlcipher
```bash
	mkdir lib
	cd lib
	git clone https://github.com/sqlcipher/sqlcipher.git --depth=1 --branch v3.4.1
	cd sqlcipher
	./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="-lcrypto"
	make
	cd ..
``` 


###Compile and run tests  
       qmake CONFIG+=tests  
       make  
       tests/unittests/unittests  


##Compilation on Windows


![windows](../img/developer/windows_logo.png "Windows")

###Qt Installation

Install Qt via: [Qt Download](http://www.qt.io/download/)  

Use default options.  
Add to the PATH environment variable

       ;C:\Qt\5.15\mingw492_32\bin;C:\Qt\Tools\mingw492_32\bin;C:\Qt\Tools\mingw492_32\opt\bin  

Depends on which version of Qt you use.   

###MSYS2 Installation

Choose your MSYS2 installer here: [MSYS2](http://msys2.github.io/)

Follow the install procedure.  
Don't forget to sync & Update pacman.  

       pacman -Syu  

Restart console  

       pacman -Su  

Install all default programs  

       pacman -S base-devel git wget p7zip gcc perl ruby doxygen cmake  

Choose only w64-x86_64 if you want only compilation in 64Bit architecture.  

       pacman -S mingw-w64-x86_64-toolchain  

###Install other binutils:   
       pacman -S mingw-w64-x86_64-miniupnpc
       pacman -S mingw-w64-x86_64-libxslt
       pacman -S mingw-w64-x86_64-xapian-core
       pacman -S mingw-w64-x86_64-sqlcipher
       pacman -S mingw-w64-x86_64-qt5-base
       pacman -S mingw-w64-x86_64-qt5-multimedia
       pacman -S mingw-w64-x86_64-ccmake
       pacman -S mingw-w64-x86_64-rapidjson
       pacman -S mingw-w64-x86_64-json-c
       pacman -S mingw-w64-x86_64-libbotan
       pacman -S mingw-w64-x86_64-asio

Add MSYS2 to PATH environment variable depends your windows  

       ;C:\msys64\mingw64\bin


###Git Installation

Install Git Gui or other client: [Git Scm](https://git-scm.com/download/win)

Create a new directory named:  

       C:\Development\GIT  

Right-click on it and choose: *Git Bash Here*  

Paste this text on git console:  

      git clone https://github.com/RetroShare/RetroShare.git  


### Compile Retroshare

Open an MSys2 64 shell  

       cd /c/Development/GIT/RetroShare/RetroShare  
       qmake
       mingw32-make

The executable produced will be:  
 
       /retroshare-gui/src/release/  

##Compilation on MacOS

![MacOS logo](../img/developer/apple_logo.png "Apple")

### Qt Installation

Install Qt via: [Qt Download](http://www.qt.io/download/)

Use default options. And add Qt Script support.

Add to the PATH environment variable by editing your *~/.profile* file.

       export PATH="/users/$USER/Qt/5.14.1/clang_64/bin:$PATH"

Depends on which version of Qt you use.

### Get RetroShare

In Qt Creator Projects -> New -> Import Project -> Git Clone -> Choose
Add Repository and Continoue

       Repository: https://github.com/RetroShare/RetroShare.git 

via Terminal:

       cd <your development directory>
       git clone https://github.com/RetroShare/RetroShare.git retroshare

via GitHub Desktop: [GitHub Desktop Download](https://central.github.com/deployments/desktop/desktop/latest/darwin)

In GitHub Desktop -> Clone Repository -> URL

       Add Repository URL: https://github.com/RetroShare/RetroShare.git and Clone

### ***Choose if you use MacPort or HomeBrew***

### MacPort Installation

Install MacPort and XCode following this guide: [MacPort and XCode](http://guide.macports.org/#installing.xcode)

Start XCode to get it updated and to enable the C compiler to create executables.

#### Install libraries  

       $ sudo port -v selfupdate
       $ sudo port install openssl
       $ sudo port install miniupnpc
       $ sudo port install libmicrohttpd
       
For VOIP Plugin: 

       $ sudo port install speex-devel
       $ sudo port install opencv
       $ sudo port install ffmpeg

Get Your OSX SDK if missing: [MacOSX-SDKs](https://github.com/phracker/MacOSX-SDKs)

### HOMEBREW Installation

Install HomeBrew following this guide: [HomeBrew](http://brew.sh/)

Install XCode command line developer tools:

       $ xcode-select --install

Start XCode to get it updated and to able C compiler to create executables.

#### Install libraries  

       $ brew install openssl
       $ brew install miniupnpc
       $ brew install libmicrohttpd
       $ brew install rapidjson
       $ brew install sqlcipher
       
If you have error in linking, run this:

       $sudo chown -R $(whoami) /usr/local/lib/pkgconfig

For VOIP Plugin: 

       $ brew install speex
       $ brew install speexdsp
       $ brew install opencv
       $ brew install ffmpeg

For FeedReader Plugin:

       $ brew install libxslt

Get Your OSX SDK if missing: [MacOSX-SDKs](https://github.com/phracker/MacOSX-SDKs)

### Last Settings

In QtCreator Projects -> Manage Kits > Version Control > Git:

       select "Pull with rebase"

In QtCreator Projects -> Build -> Build Settings -> Build Environment -> Add this path:

       /usr/local/bin

In QtCreator Projects -> Build Settings -> Build Steps -> Add Additional arguments:

       "CONFIG+=rs_autologin" "CONFIG+=rs_use_native_dialogs" 

### Set your Mac OS SDK version

Edit RetroShare.pro  

    CONFIG += c++14 rs_macos11.1

and then retroshare.pri

    macx:CONFIG *= rs_macos11.1
    rs_macos10.8:CONFIG -= rs_macos11.1
    rs_macos10.9:CONFIG -= rs_macos11.1
    rs_macos10.10:CONFIG -= rs_macos11.1
    rs_macos10.12:CONFIG -= rs_macos11.1
    rs_macos10.13:CONFIG -= rs_macos11.1
    rs_macos10.14:CONFIG -= rs_macos11.1
    rs_macos10.15:CONFIG -= rs_macos11.1


### Link Include & Libraries

Edit your retroshare.pri and add to macx-*  section

    INCLUDEPATH += "/usr/local/opt/openssl/include"
    QMAKE_LIBDIR += "/usr/local/opt/openssl/lib"
    QMAKE_LIBDIR += "/usr/local/opt/sqlcipher/lib"
    QMAKE_LIBDIR += "/usr/local/opt/miniupnpc/lib"

alternative via Terminal

    $ qmake INCLUDEPATH+="/usr/local/opt/openssl/include" QMAKE_LIBDIR+="/usr/local/opt/openssl/lib" QMAKE_LIBDIR+="/usr/local/opt/sqlcipher/lib" QMAKE_LIBDIR+="/usr/local/opt/miniupnpc/lib"

For FeedReader Plugin:

    INCLUDEPATH += "/usr/local/opt/libxml2/include/libxml2"

For building RetroShare with plugins:

    $ qmake \
    INCLUDEPATH+="/usr/local/opt/openssl/include" QMAKE_LIBDIR+="/usr/local/opt/openssl/lib" \
    QMAKE_LIBDIR+="/usr/local/opt/sqlcipher/lib" \
    QMAKE_LIBDIR+="/usr/local/opt/miniupnpc/lib" \
    INCLUDEPATH+="/usr/local/opt/opencv/include/opencv4" QMAKE_LIBDIR+="/usr/local/opt/opencv/lib" \
    INCLUDEPATH+="/usr/local/opt/speex/include" QMAKE_LIBDIR+="/usr/local/opt/speex/lib/" \
    INCLUDEPATH+="/usr/local/opt/speexdsp/include" QMAKE_LIBDIR+="/usr/local/opt/speexdsp/lib/" \
    INCLUDEPATH+="/usr/local/opt/libxslt/include" QMAKE_LIBDIR+="/usr/local/opt/libxslt/lib" \
    QMAKE_LIBDIR+="/usr/local/opt/ffmpeg/lib" \
    LIBS+=-lopencv_videoio \
    CONFIG+=retroshare_plugins \
    CONFIG+=rs_autologin \
    CONFIG+=rs_use_native_dialogs \
    CONFIG+=release \
    ..

### Compile RetroShare 

You can now compile RetroShare into Qt Creator or with Terminal

       cd retroshare
       qmake; make

You can change Target and SDK in *./retroshare.pri:82* changing value of QMAKE_MACOSX_DEPLOYMENT_TARGET and QMAKE_MAC_SDK

You can find the compiled application at *./retroshare/retroshare-gui/src/retroshare.app*

### Copy Plugins

    $ cp \
    ./plugins/FeedReader/lib/libFeedReader.dylib \
    ./plugins/VOIP/lib/libVOIP.dylib \
    ./plugins/RetroChess/lib/libRetroChess.dylib \
    ./retroshare-gui/src/RetroShare.app/Contents/Resources/
