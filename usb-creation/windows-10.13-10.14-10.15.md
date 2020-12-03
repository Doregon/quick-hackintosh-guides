# Making the installer for macOS on Windows
#### Currently High Sierra 10.13 to Big Sur 11

Support for Mac OS Extended (Journaled) is nonexistent in Windows. Because of this, you **cannot** build a full installer for macOS. However, you can build an installer for the recovery image, and all you'll need are these things:

* A 4GB flash drive
* A complete clone of the  <a href="https://github.com/corpnewt/gibMacOS">gibmacOS</a> repository
* An internet connection to download the file

## 1. Acquiring the installer

**Download the gibmacOS repository** by going to the link above and clicking Download > As .zip.
