#Compilation

##Compilation on Linux

![Linux tux logo](../img/developer/tux_logo.png "GNU/Linux")

###Install package dependencies:
#### Debian/Ubuntu
```bash
   sudo apt-get install g++ cmake qt5-qmake qtmultimedia5-dev \
   libqt5x11extras5-dev libbz2-dev libjson-c-dev libssl-dev libsqlcipher-dev \
   libupnp-dev libxss-dev rapidjson-dev libbotan-2-dev
```

Additional dependencies for Feedreader plugin:
```bash
   sudo apt-get install libxml2-dev libxslt1-dev
```

Additional dependencies for Voip plugin:
```bash
   sudo apt-get install libavcodec-dev libcurl4-openssl-dev \
   libqt5multimedia5-plugins libspeexdsp-dev
```


#### openSUSE
```bash
   sudo zypper install gcc-c++ cmake libqt5-qtbase-devel \
   libqt5-qtmultimedia-devel libqt5-qtx11extras-devel libbz2-devel \
   libopenssl-devel libupnp-devel libXss-devel sqlcipher-devel rapidjson-devel
```

Additional dependencies for plugins:
```bash
   sudo zypper install ffmpeg-4-libavcodec-devel libcurl-devel libxml2-devel \
   libxslt-devel speex-devel speexdsp-devel
```

#### Arch Linux
```bash
   pacman -S base-devel libgnome-keyring libmicrohttpd libupnp libxslt \
       libxss opencv qt4 speex sqlcipher
```

###Checkout the source code
```bash
   mkdir ~/retroshare
   cd ~/retroshare 
   git clone https://github.com/RetroShare/RetroShare.git trunk
```

###Checkout the submodules
```bash
   git submodule update --init --remote libbitdht/ libretroshare/ retroshare-webui/ supportlibs/librnp supportlibs/rapidjson
   git submodule update --init supportlibs/restbed
```

###Compile
```bash
   cd trunk
   qmake CONFIG+=release CONFIG+=rs_jsonapi CONFIG+=rs_webui CONFIG+=rs_autologin
   make
```

###Install
```bash
   sudo make install
```

The executable produced will be:  
 
 - /usr/bin/RetroShare06  
 

###For packagers

Packagers can use PREFIX and LIB\_DIR to customize the installation paths:
```bash
	qmake PREFIX=/usr LIB_DIR=/usr/lib64 "CONFIG-=debug" "CONFIG+=release"
	make
	make INSTALL_ROOT=${PKGDIR} install
```
 
 
###libsqlcipher
If libsqlcipher is not available as a package

You need to place sqlcipher so that the hierarchy is:

      retroshare
          |
          +--- trunk
          |
          +--- lib
                |
                +---- sqlcipher
```bash
	mkdir lib
	cd lib
	git clone git://github.com/sqlcipher/sqlcipher.git
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

       ;C:\Qt\5.5\mingw492_32\bin;C:\Qt\Tools\mingw492_32\bin;C:\Qt\Tools\mingw492_32\opt\bin  

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

       $xcode-select --install

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
