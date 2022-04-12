Things you will need
1. Internet
2. A Debit/Credit Card (you won't be paying for anything, it's just needed for creating an account)
3. Time
4. Patience

Things that will be helpful
1. Some Linux Experience
2. a

The instructions in this guide are directed towards Windows 10/11 users however you may still be able to follow some of the instructions provided that you are knowledgable with your operating system. The main difference comes from the way you access the servers, SSH.

With that out of the way, let's begin.

## Step 1: Create an Oracle Cloud account.
Go to https://www.oracle.com/cloud/free/ and sign up for your account. Keep your username and password in mind. This is also where you will enter your card information.

![image](https://user-images.githubusercontent.com/41555495/142959375-fa1e4dd5-6edc-475d-bd7d-82f30b83971b.png)

## Step 2: Log in to your Oracle Cloud account. 
Go to https://www.oracle.com/cloud/sign-in.html and type in the username you signed up with.

Process through the rest of the options as shown in the screenshots.
![image](https://user-images.githubusercontent.com/41555495/142959583-294cb563-fa1f-4359-88cf-17ffc4c18b83.png)
![image](https://user-images.githubusercontent.com/41555495/142959598-743d4c5d-c68b-4818-893a-122df47245e0.png)
![image](https://user-images.githubusercontent.com/41555495/142959630-6edb665f-b022-41cc-a9d3-d4ac7374cf5c.png)

## Step 3: Create a VM Instance

 Once you're at the "Get Started" page, click on "Create a VM Instance".
![image](https://user-images.githubusercontent.com/41555495/142959819-03939954-759c-4567-90f5-7159e792886f.png)

## Step 4: Set the name of your machine at the top.

Possible names would be "chserv" or "clonline" or just whatever you choose. This will be the name of the VM. For the purpose of this tutorial, I will reference the name as "clonline".
![image](https://user-images.githubusercontent.com/41555495/142959939-ad2a8614-0d0f-4125-a0c2-3be0ffc70557.png)

## Step 5: Edit the Image and shape.

Press on the "Edit" button"
![image](https://user-images.githubusercontent.com/41555495/142960009-80cca254-787c-46da-befd-aa6891334362.png)

For the purpose of this tutorial, we will be use Canonical Ubuntu so click on "Change image" on the right side and change the option from Oracle Linux to Canonical Ubuntu. Press "Select Image" once you have it selected.
![image](https://user-images.githubusercontent.com/41555495/142960072-5768c7b5-ec1d-4ee6-ac7c-cf288648294f.png)
![image](https://user-images.githubusercontent.com/41555495/142960116-035b8342-8410-42db-b972-3c9a8de2e813.png)

Press on "Change shape" on the right side.
![image](https://user-images.githubusercontent.com/41555495/142960232-74d3983b-b5d8-46e7-b099-aff5198f1ae5.png)

Change the "Shape series" from Specialy and previous generation to Ampere. Select "VM.Standard.A1.Flex". If you want to dedicate all of your free resources to one VM, set the number of OCPUs to 4 and amount of memory to 24. If you want the bare minimum, I would suggest 1 OCPU and 4gb of memory.
Press "Select shape" at the bottom once you're finished selecting.
![image](https://user-images.githubusercontent.com/41555495/142960552-b356ca34-4151-4db0-8dcc-dac7b5a94e80.png)
(ignore the service limits from the screenshot. this is solely due to me using up all my resources already)

## Step 6: Download Private Key.

In the "Add SSH keys" section, click on "Save Private Key" and save it to some location where you can access it.
![image](https://user-images.githubusercontent.com/41555495/142960658-a4feab4c-8bc7-41d8-97b3-7dbd0bf0c92a.png)

## Step 6.5: Modify the permissions of the Private Key file.

(Instructions for Windows 10/11)
Right click on the Private Key file and click on "Properties".
Click on the "Security" tab.
Click "Advanced".
Click "Disable Inheritance".
Click "Convert inherited permissions into explicit permissions on this object."
Remove each of the entries from this list EXCEPT FOR YOUR OWN USER PROFILE (will have your account name).
Press "Ok" (x2).

Instructions for other operating systems can be found [here](https://docs.oracle.com/en-us/iaas/Content/Compute/Tasks/accessinginstance.htm)

## Step 7: Finish creating the VM.

Press "Create" at the bottom of the page and wait for your machine to be done provisioning.

## Step 8: Access the VM with SSH.

(Instructions for Windows 10/11)
Once done provisioning, open up a command prompt in the same directory as your key file. You can do this by holding "Shift" and right-clicking. 
You should see something like "Open command window here" or "Open powershell window here".
Once your terminal is open, type in this command.

```
ssh -i <privatekey.key> ubuntu@<ip-here>
```
Replace <privatekey.key> with the name of your private key file and replace <ip-here> with the IP address you see in your Oracle Instance details.

Press Enter and if you see a message "Are you sure you want to keep connecting" or something similar, type "yes".
If all goes right, you should be connected to your VM.
Any future cases of connecting using this command will immediately log you in without the message in the middle.

Instructions for other operating systems can be found [here](https://docs.oracle.com/en-us/iaas/Content/Compute/Tasks/accessinginstance.htm)

## OPTIONAL STEP: Create a batch script to connect to your VM. (This will make the connection process quicker and easier)

(Instructions for Windows 10/11)
Open Notepad and copy this text.

```
@echo off
ssh -i <privatekey.key> ubuntu@<ip-here>
```

Same replacements I mentioned in Step 8 for the private key and IP address. 
Press File > Save As > Select the same directory as your private key file. 
Give the file any name and add ".bat" at the end.
Change "Save as type" from Text Documents to All Files.
Press "Save".

Open the file and it should pop up with a command window and act as described in Step 8. 
  
## Step 9: Setup the Firewall.

Type in these commands SEPARATELY.

```
sudo apt update
sudo apt install firewalld
sudo systemctl enable firewalld
sudo systemctl start firewalld
```

Depending on how many ports you want to open will affect the next step.

If you only want 1 Lobby, open the default port with this command:
```
sudo firewall-cmd --zone=public --permanent --add-port=14242/udp 
```
Alternatively if you want multiple lobbies, you'll want to open multiple ports. 

For example: If you want to open 100 ports, you could open ports 14242 to 14341 all to be used for Clone Hero Online.

This can be done with this command:
```
sudo firewall-cmd --zone=public --permanent --add-port=14242-14341/udp 
```

After adding the ports, reload the firewall with this command.
```
sudo firewall-cmd --reload
```
  
## Step 10: Install Unzip.
  
Type in this command:
```
sudo apt install unzip
```

## Step 11: Setup Network on Oracle.

Heading back to the Oracle website, click on the subnet right underneath "Primary VNIC".

Click on the text "Default Security List for <vcn name>".

Click on "Add Ingress Rules".

Put in these values: 
  - Source CIDR: 0.0.0.0/0
  - IP Protocol: UDP
  - Destination Port Range: Port and/or Port Range that you opened in Step 9.

Click on "Add Ingress Rules" again.

You may possibly need to reboot your VM in order to use the new network setup but I'm unsure. Feel free to reboot if you want or not.

## Step 12: Download the latest Clone Hero Standalone Server.

As of typing these instructions, the latest version of the PTB of Clone Hero is v1.0.0.3075.

If there is a newer version of Clone Hero, then follow these instructions.

Head to the [Clone Hero Discord](https://discord.gg/Hsn4Cgu).

Make sure you are opted in for the PTB Tester Role by reacting in the #ptb-opt-in channel

Head to the #ptb-announcements channel.

Copy the link for the latest stadalone server download posted by Matt.
  
Alternatively, You can copy the link for the standalone server for v1.0.0.3075 [here](https://pubdl.clonehero.net/chserver/ChStandaloneServer-v1.0.0.3075-master.zip).

Head back to your VM terminal and type in this command.
```
wget <paste link here>
```
The file should download and you should see it appear if you type in `ls` in the terminal.

## Step 13: Unzip the standalone server download.

Type in these commands SEPARATELY. 
```
unzip <standlone server zip file here. you can start typing it and press tab to auto-finish>
cd <standalone server folder>/linux-arm64
chmod +x ./Server
```

## Step 14: Setup a single lobby
 
You should now be able to open the server by just typing `./Server`

If you are just setting up one single lobby, running this server and following the on-screen instructions will work fine.

If you want to start the server with only one command (no on-screen instructions), then enter either of these commands:
```
No Password: ./Server -n "server name" -np -a 0.0.0.0 -p 14242
With Password: ./Server -n "server name" -ps "password" -a 0.0.0.0 -p 14242
```

You should be able to connect using the IP you've been using to connect to your VM (Also listed on your Instance details page on Oracle) and using the default port 14242.

## Step 14.5: Setup multiple lobbies.

If you are setting up multiple lobbies, enter either of these commands
```
No Password: ./Server -n "server name" -np -a 0.0.0.0 -pr <port range separated by a dash> -i <number of instances>
With Password: ./Server -n "server name" -ps "password" -a 0.0.0.0 -pr <port range separated by a dash> -i <number of instances>
```

TIP: Enter in `./Server --help` and you'll see the many arguments you can use when starting the servers.

## Step 15: Server settings.

One of the main benefits of running your own Clone Hero Online servers is to bypass the restrictions of the public servers, especially song speed limitations.

If you type in `ls`, you will notice that there are two new files: `settings.ini` and `server.log`. We're going to use one of the built-in text editors to modify the settings.

Type in `nano settings.ini`.
  
Here are the descriptions for each option
- `maxplayers` - Max number of players allowed in lobby
- `onlyhostchoosesongs` - If set to 1, only the first person who joined the lobby can add songs to the playlist (at 0, all players can)
- `maxspectators` - Max number of spectators allowed in lobby
- `servertickrate` - Server tickrate (i'm not too sure, just keep it at its default of 30 to be safe)
- `lowsongspeed` - Lowest speed that can be selected
- `maxsongspeed` - Highest speed that can be selected
- `clientremovesongs` - If set to 1, then all players can remove songs from the playlist (at 0, only the host can)
- `songsperclient` - The max amount of songs each individual player can add
- `minrequiredplayers` - The minimum number of players needed before you can start playing
  
Use the cursor to navigate the screen and modify these values as you wish.
  
When you're done, press Ctrl+X.
  
It will ask "Save modified buffer?" where you should press "Y".
 
Press enter.
  
Now the next time you run your server it will use your new settings.

## Step 16: Make server run in the background.

As you may be able to notice, you are not able to exit out of your terminal/cokmmand window without quitting out of the Server application.
  
For any of the commands listed in Step 14 or 14.5, adding "&" to the end of the command will make it run in the background and allow you to exit your terminal session.

## Step 16.5: Quitting out of your server.

If you were to connect back to your VM, you would be at the terminal with no clear way to close your server program.
  
To do this, just type in `killall -e "Server"` and it will close out of the Server program in the background.

## Step 17: Add lobby/lobbies to in-game list 
 
If you are adding 1 or 2 lobbies to your in-game list, you can add it by following these instructions
 
1. Open up Clone Hero 
2. Press Online
3. Press Join Server
4. Press the Orange fret
5. From this menu, you can add your address, port, and optional password if you set one up
6. After you press confirm it will attempt to connect and add it to your list. If it does not work, read through previous instructions and make sure you haven't skipped anything.
 
If you are adding multiple lobbies to your in-game list, you can generate a list using this web-based tool I made called [Clone Hero Online Server List Generator](https://pizzachamp.github.io/chservlistgen/). There is also an console app executable version you can download [here](https://github.com/Pizzachamp/ServerListThing). These tools assume that the ports you use are in numerical order. Once you have your list of lobbies, you'll want to add them to your "settings.ini" file in your Clone Hero Installation Folder which can be found by following these instructions
 
1. Go to the Clone Hero Launcher
2. Press Settings
3. Press Folder Icon to the right of "CloneHero Install Directory"
4. Open "settings.ini" with Notepad or some other text editor
5. Find a section named "[servers]" (if it doesn't exist, add it yourself)
6. Copy the list of servers so it's in a similar format as shown below
 
![image](https://cdn.discordapp.com/attachments/813512711877951531/963244299380744212/unknown.png)
 
# Q&A

### ***Why would I want to do this?***

Hosting your own dedicated clone hero servers that you can use with you and your friends have their own benefit. 

First, we'll compare the other choices we have in terms of playing Clone Hero Online.
  
1. Using public CH lobbies
   - Pros: Quick and easy to use, Don't need to give out your IP or use hamachi
   - Cons: Server limits (Song speed limits, number of songs per person, etc...), Having random people join your game

2. Hosting a lobby from your own PC / within Clone Hero
   - Pros: Can set your own server limits, don't have to worry about random people joining, can add password protection
   - Cons: Need knowledge about port forwarding OR have to setup using Hamachi (or other similar service), If creating the lobby within Clone Hero, if you disconnect then all players disconnect

The dedicated server method basically takes the "Pros" from both of these choices and puts them together with the only "Con" being that the initial setup can be a bit lengthy.\
  
Thankfully. this can be a mostly one-time setup where you can start the lobby and forget about it.
  
### ***Why do I need a credit/debit card?***
  
Oracle Cloud will not restrict you from using resources that are paid. Because of this, they make you put a card on your account so that in the case where you were to use more resources, they would charge you. 

You can check out Oracle Cloud's Always Free cloud services [here](https://www.oracle.com/cloud/free/#always-free).
# Special Thanks

Big thanks to [Matt](https://twitter.com/mdsitton) for making and improving on the standalone server. Makes life much simpler for us.
  
Big thanks to [BormoTime](https://twitter.com/BormoTime) for telling me about Oracle Cloud and helping me through some of my setup during my first use.
