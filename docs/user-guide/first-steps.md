# First Steps

This aims to be a Step by Step Guide for New Users. 

## Download  
Download RetroShare from [here](../user-guide/installation/).

## Install
Install RetroShare on your Computer

## Create new Profile
Start RetroShare to create your Node. 

<p style="text-align: center;">
![create new node](../img/first-steps/create_new_profile_2.png "Create New Node")  
</p>

Enter the values:  

 - Name  
   Name of your Account ([GPG-ID](../user-guide/settings/#public-information)) 
   Visible to your friends, and friends of friends. 
 - Password  
   This password protects your private PGP key. 
   It's wise to choose a long password for your GPG-ID, as this also 
   encrypts your entire RetroShare directory.  
  
Optional: (advanced options)  
 - Node Name ([Location](../user-guide/settings/#public-information))
   Each user can have several Locations were RetroShare is running on 
   different devices with the same [GPG-ID](../user-guide/settings/#public-information). 

 - Chat name  
   Name of your first Identity ([GXS-ID](../user-guide/interface/#pseudonymous-identities)) 
   Used when you write in chat lobbies, forums and channel comments. Can be setup later if you need one. 

Move your mouse to create randomness for the Key creation. 
<p style="text-align: center;">
![Enter Profile Values](../img/first-steps/enter_profile_values_new.png "Enter Profile Values")  
</p>

Sign your Certificate by entering your Password.  
<p style="text-align: center;">
![Sign your Certificate](../img/first-steps/sign_cert.png "Sign your Certificate")  
</p>

## First Start  
When you start RetroShare the first time it's empty, because there is no 
content shared by friends. This will change soon with your first connected Friend. 

<p style="text-align: center;">
![First Start](../img/first-steps/first_start.png "First Start")  
</p>

## Initial Settings
Click on the ![Options](../img/first-steps/options.png "Options") Options 
Button to change your ![Network](../img/first-steps/network.png "Network") 
Network Settings  

<p style="text-align: center;">
![Initial Settings](../img/first-steps/initial_settings.png "Initial Settings")  
</p>


   ### Nat Settings
   <p style="text-align: center;">
   ![NAT Settings](../img/first-steps/nat_settings.png "NAT Settings") 
   </p>
   
   Keep your Network Mode at *Public: DHT & Discovery*  
   This will enable DHT and Discovery to improve the connectivity. DHT is 
   also recommended to use, because it provides [Hole Punching](https://en.wikipedia.org/wiki/UDP_hole_punching) 
   and [NAT-PMP](https://en.wikipedia.org/wiki/NAT_Port_Mapping_Protocol) 
   technics to open a port in your firewall. 
   ### Network mode
   <p style="text-align: center;">
   ![Network Mode](../img/first-steps/network_mode.png "Network Mode")  
   </p>
   
   If your Router is enabling [UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play), 
   keep UPnP. UPnP enables RetroShare to open itself a port on your Router. 
   Otherwise change it to *Manually Forwarded Port* and set a manual Port Forward to your 
   [NAT](../user-guide/settings/#nat) Firewall. For manual Port forward, 
   you can choose your RetroShare port also.  
   ### Upload/download speed
   Set your download and upload speeds to fit your Internet Connection. 
   Keeping this setting below of your total speed is recommended.  
   
For detailed Network Settings explanations click [here](../user-guide/settings/#network)

### Avatar
<p style="text-align: center;">
![empty Avatar](../img/first-steps/empty_avatar.png "Empty Avatar")  
</p>

You may want to change the Avatar of your Location and set a Status message.  
<p style="text-align: center;">
![Avatar](../img/first-steps/avatar.png "Avatar")  
<sub>Click on the avatar to change it.</sub>  
 </p>

<p style="text-align: center;">
![Status](../img/first-steps/status.png "Status")  
<sub>Click on the message to change it.</sub>  
</p>

<p style="text-align: center;">
![avatar and status](../img/first-steps/avatar_status.png "Avatar and Status")  
</p>

### Identity
![People](../img/first-steps/people.png "People")  

RetroShare has already created a first [signed Identity](../user-guide/interface/#pseudonymous-identities) 
for your use in [Chatrooms](../user-guide/interface/#chat-lobbies) 
and [Forums](../user-guide/interface/#forums) and Distant Chats and Mails. 

You may want to create as many additional Identities as well if needed. 

<p style="text-align: center;">
![Identity](../img/first-steps/identity.png "signed Identity") 
</p>

To change the Avatar of your Identity right click it.  
<p style="text-align: center;">
![Edit Identity](../img/first-steps/edit_id.png "Edit Identity")  
</p>

<p style="text-align: center;">
![Edit Identity](../img/first-steps/edit_identity.png "Edit Identity")  
</p>

And change your avatar picture. 

<p style="text-align: center;">
![Edit Identity](../img/first-steps/id.png "Edit Identity")  
</p>

## First Friend
![Invite](../img/first-steps/invite.png "Invite")  

Click on the ![Invite](../img/first-steps/invite_40.png "Invite")   Invite Button. 

The fastest way is to exchange the certificates directly with your friends. 
You can also export them to a file and hand them out manually or send it by mail. 

It's important to accept each other vice versa. Your friend must add your 
certificate to his Network/Friendlist. And you need to add the certificate from 
your Friend to your Network/Friendlist.  
<p style="text-align: center;">
![Connect Wizard](../img/first-steps/connect_wizard.png "Connect Wizard")
</p>

 - ![Copy to Clipborad](../img/first-steps/copyrslink.png "Copy to Clipboard") copy to clipboard  
 - ![Save to File](../img/first-steps/document_save.png "Save to File") save to file  
 - ![Send by Mail](../img/first-steps/mail_send.png "Send by Mail") send by mail  

<p style="text-align: center;">
![Show Certificate](../img/first-steps/show_cert.png "Show Certificate")  
</p>

Share your certificate with your friend and request the certificate from 
your Friend.  

Accept your Friend's certificate.  
<p style="text-align: center;">
![Accept Certificate](../img/first-steps/accept_cert.png "Accept Certificate")  
</p>

Have a look at the details and finish.
<p style="text-align: center;">
![Make Friend](../img/first-steps/make_friend.png "Make Friend")  
</p>

Connection in Progress, your Node tries to connect to your Friend. 
![Connection in Progress](../img/first-steps/connection_progress.png "Connection in Progress")  

Your connect attempt has been successful, the connection is established. 
<p style="text-align: center;">
![Connection in Established](../img/first-steps/connection_established.png "Connection in Established")  
</p>


## First Chat
Your online Contacts(Friend Nodes) will be listed in the Network Tab. 
<p style="text-align: center;">
![Friendlist](../img/first-steps/friendlist.png "Friendlist")
 </p>

Double Clicking will start an instant Chat with your Friends. 
<p style="text-align: center;">
![Instant Chat](../img/first-steps/instant.png "Instant Chat")  
</p>
 
## First Chatroom
Subscribed [Chatrooms](../user-guide/interface/#chat-lobbies) 
from your online friends are shared to you, 
and you are free to subscribe and re-share them as well to your friends.
<p style="text-align: center;">
![Chatroom](../img/first-steps/chatroom.png "Chatroom")  
</p>

In the same manner ![Forums](../img/first-steps/forums.png "Forums") [Forums](../user-guide/interface/#forums), 
![Channels](../img/first-steps/channels.png "Channels") [Channels](../user-guide/interface/#channels), 
![Posted](../img/first-steps/posted.png "Posted") [Posted](../user-guide/interface/#posted) and 
![File Sharing](../img/first-steps/filesharing.png "File Sharing") [File Sharing](../user-guide/interface/#file-sharing) 
will become more and more available per direct 
[Friend-2-Friend](../concept/Friend-2-Friend/#retroshare) 
connections as 
[**your network**](../concept/topology/#retroshare) grows.  
