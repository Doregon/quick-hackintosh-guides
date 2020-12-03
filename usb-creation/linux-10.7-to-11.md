# Making the installer for macOS on Linux
#### Currently Lion 10.7 - Big Sur 11

Support for Mac OS Extended (Journaled) drives isn't the same in Linux, and thus we can't make a full offline installer for macOS. However, using some command line tools and a python script, we can still make a **recovery installer** to let us get macOS. To get started, you'll need:

* A 4GB flash drive
* Latest release of <a href="https://github.com/acidanthera/OpenCorePkg">OpenCorePkg</a>
* An internet connection to download the file
* dmg2img (preinstalled on Ubuntu 20.04 and later)
* (Some) knowledge of the Linux terminal
* Access to `sudo` priveliges

## 1. Aquiring the recovery installer

To get the recovery installer, download the latest release of OpenCorePkg from the repository I told you to earlier, then **open a terminal and `cd` into the Utilities/macrecovery folder**. Once that's completed, type the following commands:

* `cd Downloads` - or wherever you downloaded the python script
* `chmod +x fetch-macOS.py` - will let you run the script, **required**

Now, run one of the commands below depending on the OS you'd like to have.
**If you're downloading a version of macOS older than High Sierra**, your file will be named "RecoveryImage.dmg". If that's the case, follow all the steps but replace any instance of "BaseSystem.dmg" with "RecoveryImage.dmg"

##### Lion(10.7)  
`python ./macrecovery.py -b Mac-2E6FAB96566FE58C -m 00000000000F25Y00 download`  
`python ./macrecovery.py -b Mac-C3EC7CD22292981F -m 00000000000F0HM00 download`  

##### Mountain Lion(10.8)  
`python ./macrecovery.py -b Mac-7DF2A3B5E5D671ED -m 00000000000F65100 download`  

##### Mavericks(10.9)  
`python ./macrecovery.py -b Mac-F60DEB81FF30ACF6 -m 00000000000FNN100 download`  

##### Yosemite(10.10)  
`python ./macrecovery.py -b Mac-E43C1C25D4880AD6 -m 00000000000GDVW00 download`  

##### El Capitan(10.11)  
`python ./macrecovery.py -b Mac-FFE5EF870D7BA81A -m 00000000000GQRX00 download`  

##### Sierra(10.12)  
`python ./macrecovery.py -b Mac-77F17D7DA9285301 -m 00000000000J0DX00 download`  

##### High Sierra(10.13)  
`python ./macrecovery.py -b Mac-7BA5B2D9E42DDD94 -m 00000000000J80300 download`  
`python ./macrecovery.py -b Mac-BE088AF8C5EB4FA2 -m 00000000000J80300 download`  

##### Mojave(10.14)
`python ./macrecovery.py -b Mac-7BA5B2DFE22DDD8C -m 00000000000KXPG00 download`  

##### Catalina(10.15)
`python ./macrecovery.py -b Mac-00BE6ED71E35EB86 -m 00000000000000000 download`  

##### Big Sur (11)
`python ./macrecovery.py -b Mac-E43C1C25D4880AD6 -m 00000000000000000 download ` 


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

If you need new kexts for the release you chose but are like me and don't want to accidently delete your current OS in case something goes wrong, you can **copy your current EFI folder** to the USB's EFI partition and use that to test.
