# Making the installer for the latest version of macOS on a Mac
#### Currently macOS Big Sur 11

It's pretty simple, really. This guide will show you how to create a **full installer** for macOS (which enables you to not have to be connected to the internet at install time.) This guide works in any version of macOS from El Capitan (10.11) onwards. All you need are the following:

* A 16GB flash drive
* An internet connection

## 1. Aquiring the installer

Whether or not you're currently running the latest version, you can **download the installer from the App Store. If you're running macOS Mojave 10.14 or later**, it will open System Preferences and confirm if you want to download it.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/big-sur-full-1.png" width=75%>
</p>

## 2. Preparing to flash


Once it's downloaded, it will most likely open itself up. Because we want to make an installer, we can hit **Install macOS > Quit** in the menu bar.

Now, **open up Disk Utility** and hit the View Options button in the top left corner of the window. In that dropdown, select **Show All Devices**. Then, **find your USB** in the sidebar and select the root of it (not the partitions in it!) and select Erase. **Use Mac OS Extended (Journaled)** because the installer can't be booted from APFS drives.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/big-sur-full-4.png" width=75%>
</p>



## 3. Making the USB

Once that's all set, **open a new Terminal** session and type in the following command, where **yourvolume is your USB's new name** (if you chose more than one word for the name, put a \ and space before starting to type the second word.):

`sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/yourvolume`

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/big-sur-full-5.png" width=75%>
</p>

Once this is completed, you can safely remove your fresh new macOS Big Sur Installer USB. This one is **full** and does not require you to have an internet connection when installing macOS.


## 4. Next steps

If you need new kexts for the release you chose but are like me and don't want to accidently delete your current OS in case something goes wrong, you can **copy your current EFI folder** to the USB's EFI partition and use that to test. If a kext doesn't work under Big Sur (will probably happen to you), check out **kext.me**, a nice catalog of kexts, bootloaders, and guides for you to enjoy.
