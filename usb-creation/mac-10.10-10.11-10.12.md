# Making the installer for earlier versions of macOS on a Mac
#### Yosemite 10.10 to Sierra 10.12

If you can't use High Sierra 10.13 or newer, but need Yosemite 10.10, El Capitan 10.11, or Sierra 10.12, you can make a **full** installer (which enables you to not have to be connected to the internet at install time.)  
**This guide works on any version of macOS in the following:

Upgrading to Yosemite 10.10 **requires Mac OS X Snow Leopard 10.6.8 up to Mavericks 10.9.5.**   
Upgrading to El Capitan 10.11 **requires Mac OS X Snow Leopard 10.6.8 up to Yosemite 10.10.5.**  
Upgrading to Sierra 10.12 **requires Mac OS X Snow Leopard 10.6.8 up to El Capitan 10.11.6.**  

All you need are the following:

* A 8GB flash drive
* An internet connection

## 1. Aquiring the installer

You may notice that you can't exactly take a trip to the App Store and download these versions anymore, because Apple no longer supports them. To get them, **go to this <a href="https://support.apple.com/en-us/HT211683">Apple Support</a> page and select the version you want** to download the InstallOS.dmg (Sierra) or InstallMacOSX.dmg (Yosemite and El Capitan) file.

Once the installer is downloaded, **double-click it** to mount the disk image, and **run the installer .pkg file** to extract the Installer app to your Applications folder.

## 2. Preparing to flash

Now, **open up Disk Utility** and hit the View Options button in the top left corner of the window. In that dropdown, select **Show All Devices**. Then, **find your USB** in the sidebar and select the root of it (not the partitions in it!) and select Erase. **Use Mac OS Extended (Journaled)** because the installer can't be booted from other format drives.

## 3. Making the USB


Once that's all set, **open a new Terminal** session and type in the following command, depending on your downloaded OS version, where **yourvolume is your USB's new name** (if you chose more than one word for the name, put a \ and space before starting to type the second word.):

Sierra 10.12:  
`sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  
El Capitan 10.11:  
`sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  
Yosemite 10.10:  
`sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`  

Once this is completed, you can safely remove your fresh new macOS Big Sur Installer USB. This one is **full** and does not require you to have an internet connection when installing macOS.


## 4. Next steps

If you need new kexts for the release you chose but are like me and don't want to accidently delete your current OS in case something goes wrong, you can **copy your current EFI folder** to the USB's EFI partition and use that to test. If a kext doesn't work with the OS release you selected, check out **kext.me**, a nice catalog of kexts, bootloaders, and guides for you to enjoy.
