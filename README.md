# evga-z270-stinger-hackintosh-guide
A guide for installing macOS Sierra on an EVGA Z270 Stinger motherboard and i7-7700k

## Step 1: Download macOS Sierra
On a separate Mac, veriy that you are up to date (at least 10.12.6).
![image](https://user-images.githubusercontent.com/1683528/30447848-073ba4b8-9942-11e7-962b-83fb0e4cc110.png)

Find macOS Sierra in the App Store ([direct link](https://itunes.apple.com/us/app/macos-sierra/id1127487414?mt=12)) and download it.
![image](https://user-images.githubusercontent.com/1683528/30448242-1410d7b6-9943-11e7-875b-3b3e924c92b6.png)

Quit the installer when it opens.
![image](https://user-images.githubusercontent.com/1683528/30448617-e57ac384-9943-11e7-9a3d-c2027b2b7caf.png)

## Step 2: Create Bootable USB
Plug an 8+ GB flash drive in.

In /Applications/Utilities/**Terminal.app**, run `diskutil list` to find your disk identifier. Be sure, because we will be erasing this disk. For example, in the below screenshot my disk identiier is 1. 
![image](https://user-images.githubusercontent.com/1683528/30448363-792c64ee-9943-11e7-8ff8-d60f39420dcd.png)

Run the following and replace `#` with your flash drive's disk identifier.
```
  diskutil partitionDisk /dev/disk# GPT JHFS+ "USB" 100%
```
You should now see a volume named "USB". Now run the following command to move macOS Sierra onto the drive. This command may take 30-40 minutes.
```
  sudo "/Applications/Install macOS Sierra.app/Contents/Resources/createinstallmedia" --volume /Volumes/USB --applicationpath "/Applications/Install macOS Sierra.app" --nointeraction
```

Download the latest version of the Clover EFI bootloader ([direct link](https://sourceforge.net/projects/cloverefiboot/files/latest/download?source=files)) and run it. (I used [Clover_v2.4k_r4200](https://sourceforge.net/projects/cloverefiboot/files/Installer/Clover_v2.4k_r4200.zip/download))

Click *Continue* twice, and then *Change Install Location...* to select your flash drive.
![image](https://user-images.githubusercontent.com/1683528/30450096-b131a168-9945-11e7-81e5-fda48c18ca9a.png)

Click *Continue* again and then click *Customize* and check "Install or UEI booting only"
![image](https://user-images.githubusercontent.com/1683528/30450149-d7581b9c-9945-11e7-8549-76febcebe104.png)

Then click *Install* to complete the Clover installation.
