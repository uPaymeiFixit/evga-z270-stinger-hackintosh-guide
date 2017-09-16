# Sierra Hackintosh Guide for EVGA Z270 Stinger (200 series)
A guide for installing macOS Sierra on an EVGA Z270 Stinger motherboard and i7-7700k

This guide will show you how to install **macOS Sierra 10.12.6** on a desktop running an EVGA Z270 Stinger motherboard. There are no changes made to the operating system partition, resulting in a very *vanilla* and therefore upgradable experience. For best results, use the hardware listed below.

## Hardware
- [EVGA Z270 Stinger (111-KS-E272-KR)](https://www.evga.com/products/product.aspx?pn=111-KS-E272-KR)
- [i7-7700k](https://ark.intel.com/products/97129/Intel-Core-i7-7700K-Processor-8M-Cache-up-to-4_50-GHz)
- [Asus GTX 670 4GB (GTX670-DC2-4GD5)](https://www.asus.com/us/Graphics-Cards/GTX670DC24GD5/)
- [Samsung 960 EVO NVMe M.2 500GB](http://www.samsung.com/us/computing/memory-storage/solid-state-drives/ssd-960-evo-m-2-500gb-mz-v6e500bw/)

Note: This guide may need to be tweaked or similar hardware, such as any other 200 series motherboard. Any (or no) NVMe drive, any Kaby Lake CPU, and any GPU will likely work as is. 

## What works
- [x] GPU hardware acceleration
- [x] — Metal Support
- [x] NVMe
- [x] — TRIM Support
- [x] Hardware sensors
- [x] Audio
- [x] — HDMI Audio
- [x] — All 5 analog in/out ports
- [x] Ethernet
- [x] Sleep
- [x] — Enters low power mode
- [x] — Audio wakes up
- [x] — Ethernet wakes up
- [x] — Video wakes up
- [x] Shutdown
- [x] — Stays shut down
- [x] — CMOS does not reset
- [x] USB
- [x] — USB 3.0
- [x] — USB 3.1
- [x] — USB-C

## What doesn't work
- [ ] iMessage / Facetime
- [ ] Power button
- [ ] Wi-Fi (AW-CB210NF-P)
- [ ] Bluetooth

# Instructions
## Step 1: Download macOS Sierra
On a separate Mac, verify that you are up to date (at least 10.12.6).
![image](https://user-images.githubusercontent.com/1683528/30447848-073ba4b8-9942-11e7-962b-83fb0e4cc110.png)

Find macOS Sierra in the App Store ([direct link](https://itunes.apple.com/us/app/macos-sierra/id1127487414?mt=12)) and download it.
![image](https://user-images.githubusercontent.com/1683528/30448242-1410d7b6-9943-11e7-875b-3b3e924c92b6.png)

Quit the installer when it opens.
![image](https://user-images.githubusercontent.com/1683528/30448617-e57ac384-9943-11e7-9a3d-c2027b2b7caf.png)

## Step 2: Create Bootable USB
#### Format Flash Drive
Plug an 8+ GB flash drive in.

In /Applications/Utilities/**Terminal.app**, run `diskutil list` to find your disk identifier. Be sure, because we will be erasing this disk. For example, in the below screenshot my disk identiier is 1. 
![image](https://user-images.githubusercontent.com/1683528/30448363-792c64ee-9943-11e7-8ff8-d60f39420dcd.png)

Run the following and replace `#` with your flash drive's disk identifier.
```
  diskutil partitionDisk /dev/disk# GPT JHFS+ "USB" 100%
```
You should see a volume named "USB". Now run the following command to move macOS Sierra onto the drive. This command may take 30-40 minutes.
```
  sudo "/Applications/Install macOS Sierra.app/Contents/Resources/createinstallmedia" --volume /Volumes/USB --applicationpath "/Applications/Install macOS Sierra.app" --nointeraction
```

#### Install Clover
Download the latest version of the Clover EFI bootloader ([direct link](https://sourceforge.net/projects/cloverefiboot/files/latest/download?source=files)) and run it. (I used [Clover_v2.4k_r4200](https://sourceforge.net/projects/cloverefiboot/files/Installer/Clover_v2.4k_r4200.zip/download))

Click *Continue* twice, and then *Change Install Location...* to select your flash drive.
![image](https://user-images.githubusercontent.com/1683528/30450096-b131a168-9945-11e7-81e5-fda48c18ca9a.png)

Click *Continue* again and then click *Customize* and check "Install or UEI booting only"
![image](https://user-images.githubusercontent.com/1683528/30450149-d7581b9c-9945-11e7-8549-76febcebe104.png)

Then click *Install* to complete the Clover installation.

#### Update Clover Configuration
Open the *EFI* partition created by Clover, and replace the *CLOVER* folder with the most recent *CLOVER* folder [here](). 

This will replace the `config.plist` file with the one I have created as well as install needed kexts. The `config.plist` file I created contains only the minimum configuration needed for a completely working system. I spent many hours testing many configurations and making sure only what was necessary was added. If you want to use more up-to-date kexts, view the *Sources* sectian at the bottom.

## Step 3: Conigure BIOS
During boot, press F2 to enter BIOS. Navigate to the *ADVANCED* tab and then click on *CPU Configuration*. Set *Intel(R) Virtualization Technology For Directed I/O* to *Disabled*. 

Set the primary boot device to USB Hard Disk.

Now press F10 to save and exit setup. Alternatively, you may apply the BIOS backup I created [here]().

## Step 4: Install macOS
#### Installation
With the flash drive plugged in, boot the computer. If all goes well, you should be at the macOS installer screen. When the two part installer finishes, boot the computer one more time with the flash drive still plugged in. 

You should now see your new macOS install as a bootable option in Clover. Select it and wait for it to boot. After logging in, 

#### Install Clover
Download the latest version of the Clover EFI bootloader ([direct link](https://sourceforge.net/projects/cloverefiboot/files/latest/download?source=files)) and run it. (I used [Clover_v2.4k_r4200](https://sourceforge.net/projects/cloverefiboot/files/Installer/Clover_v2.4k_r4200.zip/download))

Click *Continue* twice, and then *Change Install Location...* to select your macOS installation.
![image](https://user-images.githubusercontent.com/1683528/30450096-b131a168-9945-11e7-81e5-fda48c18ca9a.png)

Click *Continue* again and then click *Customize* and check "Install or UEI booting only"
![image](https://user-images.githubusercontent.com/1683528/30450149-d7581b9c-9945-11e7-8549-76febcebe104.png)

Then click *Install* to complete the Clover installation.

#### Update Clover Configuration
Open the *EFI* partition created by Clover, and replace the *CLOVER* folder with the most recent *CLOVER* folder [here](). 

This will replace the `config.plist` file with the one I have created as well as install needed kexts. The `config.plist` file I created contains only the minimum configuration needed for a completely working system. I spent many hours testing many configurations and making sure only what was necessary was added. If you want to use more up-to-date kexts, view the *Sources* sectian at the bottom.

# Kexts / Patches / Sources
- [NVMe Kext Patch (config.plist)](https://pikeralpha.wordpress.com/2016/06/27/nvmefamily-kext-bin-patch-data/comment-page-1/#comment-5855) from Pike R. Alpha
- [ACPISensors.kext, CPUSensors.kext, FakeSMC.kext, GPUSensors.kext, LPCSensors.kext](http://www.hwsensors.com/releases) from HWSensors Project (Binaries)
- [HDMIAudio.kext](https://github.com/toleda/audio_CloverHDMI) from Toleda
- [IntelMausiEthernet.kext](https://github.com/Mieze/IntelMausiEthernet) from Mieze
- [Lilu.kext](https://github.com/vit9696/Lilu) from vit9696
- [AppleALC.kext](https://github.com/vit9696/AppleALC/releases) from vit9696
- [NvidiaGraphicsFixup.kext](https://sourceforge.net/projects/nvidiagraphicsfixup/) from lvs1974
- [USBInjectAll.kext, XHCI-200-series-injector.kext](https://github.com/RehabMan/OS-X-USB-Inject-All) from RehabMan
