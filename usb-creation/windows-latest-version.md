# Making the installer for macOS on Windows
#### Currently Big Sur 11

All of us Hackintoshers knew everything was going to change at WWDC20. I watched the entire thing and then watched it again to confirm it--Mac OS X was gone, and Apple's relationship with Intel was ending. Two years for a transition to ARM-based Macs, and then... that's it.

We're starting to see some major changes with Big Sur. Not just the user interface, or Control Center, or even the apps themselves. Apple has restructured the software update catalog for macOS with Big Sur, originally breaking gibMacOS and making the process to create a bootable USB for it a bit harder. 

As of right now, **to my knowledge**, there's no way to make a Big Sur USB on a Windows machine. Yes, you can download the installer, but you can't use MakeInstall.bat to automate the creation of a USB anymore. These guides are meant to keep everything as simple as possible for the end user, so they aren't afraid of building a Hackintosh because it's intimidating...and the easiest way is to not even use Windows at all.

And because of the way Apple reorganized their software update catalog alongside the release of Big Sur, means that they're not changing it back any time soon. So this applies to any release starting from Big Sur **until gibMacOS's MakeInstall feature gets updated**, for support to extract the InstallAssistant.pkg file or even the BaseSystem.dmg file.

But, I've found an easy solution. For this one, you'll need to have:

* VirtualBox 6
* VirtualBox Extension Pack
* A 4GB flash drive
* An internet connection
* Some patience

## 1. Getting ready

**Install VirtualBox** on your computer.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-1.png" width=50%>
</p>

Once VirtualBox is installed, go to File > Preferences and select the Extensions tab. **Click the Add Extension button** and locate the .vbox-extpack file you downloaded.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-2.png" width=75%>
</p>

Now head over to the **Ubuntu downloads** page and choose to download Ubuntu Desktop (20.04 or 20.10 works)

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-3.png" width=75%>
</p>

**NOTE:** XD I had to switch to my Hackintosh because you can't run a VM inside a VM. The instructions still work in Windows, though.

Back in VirtualBox, enter the Create dialog to make a new virtual machine, and **select the "Expert Mode"** button at the bottom of the window. Set the memory to an **amount over 4GB**, and **change the hard disk option** to "Do not add a virtual hard disk". Also make sure you put a name and **set the OS type to Linux with Ubuntu (64-bit)** as the version

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-4.png" width=75%>
</p>

Hit the "Create" button but **don't start it!** Go to the virtual machine's Settings window and apply the following:

##### System category

`Enable EFI (special OSes only) --> enabled`

`Processors` --> at least 2 or more

##### Storage category

Under the existing `Controller: IDE` entry,
* Point the existing CD-ROM drive to the Ubuntu installation iso to add it to the virtual machine (once it's done downloading, of course).
* Select the Add CD-ROM button next to the SATA name and choose "Leave Empty"

##### Ports category

`USB --> USB 3.0 (xHCI) Controller`

Now, start the virtual machine. **It should present you with the GRUB menu**, if you set it up correctly.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-5.png" width=75%>
</p>

Select the first option (marked "Ubuntu") and wait for it to boot. **When it displays the following screen**, select "Try Ubuntu".

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-6.png" width=75%>
</p>

In the menu bar (displays right under the virtual machine's title bar on Windows) click Devices and select **Insert Guest Additions CD Image** in the dropdown that shows.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-7.png" width=50%>
</p>

Next, type the following commands **(once the system recognizes the CD image)**. This will install the VirtualBox Guest Additions files to the Ubuntu guest, and it's required to continue. 

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-8.png" width=75%>
</p>

Now, in the menu bar, **select Devices > USB** and find your USB in the list of them attached to your PC.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-virtualbox-9.png" width=75%>
</p>

Once you've successfully gotten the USB passed through to the Ubuntu virtual machine, **follow the steps listed in the Linux guides to make your installer.**
