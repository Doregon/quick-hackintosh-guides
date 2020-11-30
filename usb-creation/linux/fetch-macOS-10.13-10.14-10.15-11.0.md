# Making the installer for macOS
#### Currently High Sierra 10.13 - Big Sur 11

Support for Mac OS Extended (Journaled) drives isn't the same in Linux, and thus we can't make a full offline installer for macOS. However, using some command line tools and a python script, we can still make a **recovery installer** to let us get macOS. To get started, you'll need:

* A 4GB flash drive
* fetch-macOS-v2.py from <a href="https://github.com/kholia/OSX-KVM">this</a> repository
* An internet connection to download the file
* dmg2img (preinstalled on Ubuntu 20.04 and later)
* (Some) knowledge of the Linux terminal
* Access to `sudo` priveliges

## 1. Aquiring the recovery installer

To get the recovery installer, download the **fetch-macOS-v2.py** file from the repository I told you to earlier. Once that's completed, type the following commands:

* `cd Downloads` - or wherever you downloaded the python script
* `chmod +x fetch-macOS-v2.py` - will let you run the script, **required**

Now run the script by typing `./fetch-macOS-v2.py`. Type the number of the macOS release you wish to download (in this case, I choose 4), and it **will grab the recovery image for you.**

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-1.png" width=75%>
</p>

## 2. Preparing to flash

Once the recovery image is downloaded, type `dmg2img -l BaseSystem.dmg` to **list the partitions** in it. You'll see something like this. What we want to see is the **partition marked `disk image`**, which (in this case) is partition **5**

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-2.png" width=75%>
</p>

Now that you know which partition the recovery disk image is located on, **connect your USB**, wait for it to mount, and then type `lsblk` to list the drive blocks on your system. **Your USB will probably be located on an sdX block.**

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-3.png" width=75%>
</p>

Once you **identify your USB's block mount point**, type in `sudo gdisk /dev/sdX` (where the X is the third letter in your USB's mount point name). You'll be presented **with a screen similar to this.**

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-4.png" width=75%>
</p>

Type `o` to add a protective MBR overwrite task to the queue. It will **warn that it will delete all partitions.** Press `y` to confirm.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-5.png" width=75%>
</p>

Next, type `n` to create a new partition, and set the following parameters to make an EFI partition:

* `Partition number:` leave blank  
* `First sector:` leave blank  
* `Last sector:` +200M  
* `Hex code:` 0700 (Microsoft Basic Data)  

Type `n` again, and set these parameters to make the recovery installer partition:

* `Partition number:` leave blank  
* `First sector:` leave blank  
* `Last sector:` leave blank  
* `Hex code:` af00 (Apple HFS+)  

Once that's all done, type `w` to write your changes. It will warn you once more, press `y` to confirm that you want to format the USB. Once it's finished, it will automatically exit **and tell you that the old partition table is still being used.** To fix this, run `partprobe /dev/sdX` in your terminal or unplug/replug your USB. If those don't work, a simple reboot works too. (It's not doing it in my case because I'm using the same partition sizes.)

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-6.png" width=75%>
</p>

## 3. Making the USB

Now, it's all formatted and ready for you to flash the image. Type in `sudo dmg2img -p Y -i BaseSystem.dmg -o /dev/sdX2`, where **Y is the partition number you gathered earlier, and X is still the third letter of the USB device block.** This will write the contents of the recovery image onto the USB's Apple HFS+ partition. This could take a while, I'm using a solid state drive and it took about 2-3 minutes.

<p align=center>
<img src="https://raw.githubusercontent.com/Doregon/hackintosh-guides/main/images/fetch-on-linux-7.png" width=75%>
</p>

## 4. Next steps

If you need new kexts for the release you chose but are like me and don't want to accidently delete your current OS in case something goes wrong, you can **copy your current EFI folder** to the USB's EFI partition and use that to test. If a kext doesn't work with the OS release you selected, check out **kext.me**, a nice catalog of kexts, bootloaders, and guides for you to enjoy.
