# Making the installer for earlier versions of macOS on a Mac
#### High Sierra 10.13 to Catalina 10.15

If you can't use the latest version of macOS but need macOS High Sierra 10.13, Mojave 10.14, or Catalina 10.15, you can make a **full** installer (which enables you to not have to be connected to the internet at install time.)  
**This guide works on any version of macOS in the following**:

Upgrading to High Sierra 10.13 **requires OS X Lion 10.7.5 up to Sierra 10.12.6.**   
Upgrading to Mojave 10.14 **requires OS X Mountain Lion 10.8 up to High Sierra 10.13.6.**  
Upgrading to Catalina 10.15 **requires OS X Mavericks 10.9 up to Mojave 10.14.6.**  

All you need are the following:

* A 8GB flash drive
* An internet connection

## 1. Aquiring the installer

You may notice that you can't exactly take a trip to the App Store and download these versions anymore, because the latest version has probably replaced them. To get them, **go to this <a href="https://support.apple.com/en-us/HT211683">Apple Support</a> page and select the version you want** to open the App Store link.

## 2. Preparing to flash


Once it's downloaded, it will most likely open itself up. Because we want to make an installer, we can hit **Install macOS > Quit** in the menu bar.

Now, **open up Disk Utility** and hit the View Options button in the top left corner of the window. In that dropdown, select **Show All Devices**. Then, **find your USB** in the sidebar and select the root of it (not the partitions in it!) and select Erase. **Use Mac OS Extended (Journaled)** because the installer can't be booted from APFS drives.


## 3. Making the USB


Once that's all set, **open a new Terminal** session and type in the following command, depending on your downloaded OS version, where **yourvolume is your USB's new name** (if you chose more than one word for the name, put a \ and space before starting to type the second word.):

Catalina 10.15:  
`sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  
Mojave 10.14:  
`sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  
High Sierra 10.13:  
`sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  

Once this is completed, you can safely remove your fresh new macOS Big Sur Installer USB. This one is **full** and does not require you to have an internet connection when installing macOS.


## 4. Next steps

If you need new kexts for the release you chose but are like me and don't want to accidently delete your current OS in case something goes wrong, you can **copy your current EFI folder** to the USB's EFI partition and use that to test. If a kext doesn't work with the OS release you selected, check out **kext.me**, a nice catalog of kexts, bootloaders, and guides for you to enjoy.
