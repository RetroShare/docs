# Standard Plugins
The following plugins are generally part of downloaded/installed packages and are included with the standard source code downloads. You may need to download and install additional development libraries to compile.

## VOIP

VOIP provides video and voice communications with other friends who have the facilities. 

To compile and use (for GNU/Linux):

    cd [your retroshare source folder]/plugins/VOIP
    qmake && make clean && make
    cp lib*.so ~/.retroshare/extensions6

Restart RetroShare, enabling the plugin when asked. You can change settings in Options->VOIP.

## FeedReader

FeedReader acts as an RSS feed collector for RetroShare, gathering selected news feeds into RetroShare.

To compile and use (for GNU/Linux):

    cd [your retroshare source folder]/plugins/FeedReader
    qmake && make clean && make
    cp lib*.so ~/.retroshare/extensions6

Restart RetroShare, enabling the plugin when asked. You can change settings in Options->FeedReader.


## RetroChess

RetroChess lets you play a game of chess against a friend.

Source: <https://github.com/RetroShare/RetroChess>


# Additional Plugins

## FileInfoTaskbar
RetroShare plugin for displaying file download status on the Windows Taskbar

Works with 0.6.6 and Qt5, from <https://github.com/hunbernd/FileInfoTaskbar>

## RetroGit
RetroGit is a decentralized Git collaboration plugin for RetroShare.

From <https://github.com/defnax/retroGit>

## FriendsMap
FriendMap for RetroShare using a local GeoIP database. Displays a globe with the location of your friends on it.

From <https://github.com/RetroShare/FriendsMap>

## QtPaint
Paint plugin for RetroShare chat rooms.

From <https://github.com/RetroShare/QtPaint>

## Lua4RS
Run Lua scripts inside RetroShare to do different tasks.

From <https://github.com/defnax/Lua4RS>

## Discord Bridge
Bridges RetroShare and Discord.

From <https://github.com/defnax/discord>

## RetroAI
A RetroShare plugin that answers chat messages using a language model running on your own computer (Ollama).

From <https://github.com/defnax/RetroAI>
