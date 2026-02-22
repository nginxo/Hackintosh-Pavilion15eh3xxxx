# Hackintosh-Pavilion15eh3xxxx
Hackintosh for the HP Pavilion 15-eh3xxxx (Ryzen 7 7730U)

This hackintosh boots up to Sonoma (tested), however Tahoe is untested.
Made originally for Ventura (works best in terms of optimization and performance)

SPECS:
CPU: Ryzen 7 7730U with Radeon Graphics
RAM: 16GB 3200MHz
SSD: 512GB NVMe

BUGS / WHAT DOESN'T WORK:
- Wi-Fi
- Bluetooth
- Audio (can work by playing with the alcid=11 value in the startup settings)
- Fingerprint
- Trackpad sometimes doesn't work
- Sometimes freezes and unstable on Sonoma

NOT TESTED:
- iCloud services

HOW TO INSTALL:
Get yourself a 32GB usb drive and follow this guide.
Create two partitions on the USB,
first one should be 8GB and formatted to FAT32
second one called UnPlugged should be the whole unused space and formatted to exFAT

Once done, download UnPlugged.command from their GitHub (search UnPlugged Hackintosh Repo Github on Google)
This will be used since the online installer won't work due to the missing WiFi kext.

Download the Recovery Environment using macrecovery: THIS MUST BE VENTURA! Versions above Ventura don't allow mounting exFAT partitions, there's a workaround but you'll just make your life harder.
Once downloaded, place it in the FAT32 partition, along with the EFI. the root must have the following scheme:

/ USB - FAT32
|   com.apple.recovery.boot
|   EFI

Now we're done with this partition and we can download the whole macOS offline installer!
Download gibMacOS from their GitHub and open it: you can choose any version, however it will work best on Ventura and above
Don't worry about recovery and installer mismatches: you just need Ventura's recovery environment to mount the other partition.
Once downloaded, go on macOS Downloads/publicrelease/(your downloaded macOS version) and copy all files that are inside. These need to be placed in the exFAT partition, along with the UnPlugged.command that we downloaded earlier.
The root must have the following scheme:

/ UnPlugged - exFAT
|   InstallInfo.plist
|   com_apple_MobileAsset_MacSoftwareUpdate.plist
|   MajorOSInfo.pkg
|   InstallAssistant.pkg
|   UpdateBrain.zip
|   UnPlugged.command


GREAT! Now we're ready for installation.
Boot into your Boot selector and choose your USB, it will launch you into OpenCore's boot menu. Press SPACE and choose what ends with (external) (dmg). The first part depends on the name that your USB has.
Once booted, go to Disk Utility, partition your disk and afterwards go to Tools/Utilities to open the terminal

FOLLOW THESE STEPS CAREFULLY!
- Type cd /Volumes/UnPlugged
- Type ./UnPlugged.command
