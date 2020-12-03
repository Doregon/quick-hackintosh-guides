# Making the installer for macOS on Windows
#### Currently High Sierra 10.13 to Catalina 10.15

Support for Mac OS Extended (Journaled) is nonexistent in Windows. Because of this, you **cannot** build a full installer for macOS. However, you can build an installer for the recovery image, and all you'll need are these things:

* A 4GB flash drive
* A complete clone of the  <a href="https://github.com/corpnewt/gibMacOS">gibmacOS</a> repository
* An internet connection to download the file
* Python

## 1. Acquiring the installer

**Download the gibmacOS repository** by going to the link above and clicking Download > As .zip.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-1.png" width=75%>
</p>

Next, extract the repository and open up the `gibMacOS.bat` file inside. **If Windows SmartScreen pops up**, click "More Info" and then "Run Anyway".

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-2.png" width=75%>
</p>

In this new command prompt window, **if it doesn't find the required dependencies** that are required to run the batch file properly, it will install them for you.
Now you should be presented with a list of options. Type `i` and hit enter to toggle the "Only Show URLs" feature, we only need one file. 

**NOTE: If you want Big Sur, don't follow this guide** as it will not work for you! 

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-3.png" width=75%>
</p>

**Type the number of the version you want** to install on your PC. In this case, I've typed `2`. As you can see, a list of URLs shows up with names attached to them. We want to focus on the **RecoveryHDMetaDmg.pkg** file, so copy the URL to your clipboard with Ctrl+C.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-4.png" width=75%>
</p>

**Paste the link** into your web browser's address bar or use `curl` in the command prompt to download the file.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-5.png" width=75%>
</p>

## 2. Preparing to flash

Next, we'll open **MakeInstall.bat** and let it download any dependencies as we continue, so it's ready when we need it.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-6.png" width=75%>
</p>

Open **Disk Management** with Win+X and selecting its name in the menu that shows. Locate your USB and delete any partitions on it marked **`Basic Data Partition`**.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-7.png" width=75%>
</p>

Once you've obliterated any BDP partitions on your USB, **return to MakeInstall.bat** and find your USB in the list above the options help text. Type `XO`, where X is the number that's next to your USB's name. It will confirm that you want to overwrite this USB (type `y` to continue) and then ask for the location of the **RecoveryHDMetaDmg.pkg** file we downloaded earlier.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-8.png" width=75%>
</p>

Open File Explorer and navigate to the location where you downloaded the file, **making sure that you start at the "This PC" folder**. Once you're in the folder, **copy the address** in the "cookie crumble" navigation bar at the top.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-9.png" width=75%>
</p>

**Paste this address into** the MakeInstall.bat window and hit Enter to continue. It'll run a reformat and a decompression, and **automatically flash the image** to your USB. Once it's complete, you'll see a screen similar to this.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-10.png" width=75%>
</p>

Now you can add your Clover/OpenCore EFI folder to the new **BOOT** partition that shows up in File Explorer. You can still use the EFI on the hard drive to install, however it's easier to test your configuration if you use the USB.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/win-recoveryhdmeta-11.png" width=75%>
</p>
