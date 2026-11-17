#Create new Location
##How to create a second location for an existing user account

If you want to use your RetroShare User account accross different 
Devices, for example on your PC, Laptop, NAS, Raspberry Pi , …  
its not necessary to create different Accounts for each device. 
It’s possible to create with the same user different locations, 
which are recognized by your friends as owned by your User automatically. 
This avoids the additional Key Exchange with all your friends when you 
use RetroShare on a new device. Each location can connect to friends 
where your User account is already in the friended.


Creating a new location with the same user is easy, if you know how.  

##Let’s start with a small example between Bunny, Alice and the RedQueen.  

Bunny owns his first location “hole” and is connected with 
Alice/Wonderland and RedQueen/Hive. On Bunny’s new PC he creates a 
new RetroShare node and imports his contacts from the first node. 
Bunny's friends do not need to take care to add the new location, it 
just gets listed at Bunny’s nodes in their contact list.  

 
If you want to do it similar to bunny, Its now explained in a 
Step by Step Guide.  

 

###Step 1: Export your profile on the first node

On your first node open **Preferences** → **Node**. In the **Profile**
section click **Export profile**.

![Export profile](../img/tutorial/exportprofile.png "Export profile")

Save it with the file ending `.asc`.

This file contains the private PGP key of your RetroShare profile. With it
you can create new nodes for the same profile. Keep it safe and don't
share it with anyone.

###Step 2: Export your friend list on the first node

On the same page click **Export friends list** and save the `.xml` file.

![Export friends list](../img/tutorial/exportfriendslist.png "Export friends list")

(You can also do this in the **Network** tab: right-click in the friend
list and choose **export friendlist**.)

Copy both files (`.asc` and `.xml`) to the second computer, for example
with a USB stick.

###Step 3: Create the new node on the second computer

Start RetroShare on the second computer. The **Create new Retroshare node**
window opens. (If RetroShare already has a profile, click
**Manage profiles and nodes...** in the login window to get there.)

![Create new location](../img/tutorial/create_location_import.png "Create new location")

1. Tick **advanced options**.
2. Tick **Use existing profile...**.
3. Click **Import profile** and select your `.asc` file.

RetroShare confirms that the profile was imported:

![Profile imported](../img/tutorial/imported.png "Profile imported")

Click **OK**. Your profile is now selected. Then:

- enter a name for the new node (location), for example `Laptop`,
- enter the **password of your profile** (the same password as on your
  first node),
- move the mouse until the progress bar is full,
- create the node.

Now your new node works, but its friend list is still empty.

###Step 4: Import your friend list on the new node

Log in, go to the **Network** tab, right-click in the friend list and
choose **import friendlist**. Select the `.xml` file from your first node.

![import friendlist](../img/tutorial/import.png "Import friendlist")

![Done](../img/tutorial/done.png "Done")

Your friends from your first location are now available on your second 
location. Your first node and your second node are also friended.

![finished](../img/tutorial/finished.png "finished")  

Alice and RedQueen are now able to see the new location of Bunny.

![friendview](../img/tutorial/friendview.png "friendview")  

Thanks to sehraf for implementing the Export/Import Tool.

<sub>from <a href="https://blog.cavebeat.org/2015/09/how-to-create-a-second-location-for-an-existing-user-account/">blog.cavebeat.org</a> <a href="http://creativecommons.org/licenses/by-sa/4.0/">CC BY-SA 4.0</a></sub>
