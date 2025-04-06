# Installing Windows on the Redmi Note 13 Pro

## Prerequisites
1. **Windows on ARM Image (WoA)**  
   Download the Windows ARM image (ESD or WIM): [Windows ARM Image](https://worproject.com/esd).  

2. **Redmi Note 13 Pro Drivers**  
   You need device-specific drivers to ensure hardware compatibility. (Provide/download the drivers as an archive.)

3. **Orange Fox Recovery**  
   Ensure OFOX is installed. If not, download a compatible version for Redmi Note 13 Pro and flash it using fastboot.  

---

## Booting into OFOX
If TWRP gets replaced with stock recovery during reboot, reflash it in fastboot:
```cmd
fastboot flash recovery path\to\ofox.img
fastboot reboot recovery
```
---

Disk Management (Diskpart)

> WARNING: Do NOT modify partitions in Diskpart!
Changing partitions can brick your device permanently.



Select the Windows Partition

Find the Windows partition using:

diskpart
list volume
select volume $

Replace $ with the WINGARNET volume number.

Assign Letter X to the Windows Partition

assign letter x

Select the ESP Partition

Find the ESP partition using:

list volume
select volume $

Replace $ with the ESPGARNET volume number.

Assign Letter Y to the ESP Partition

assign letter y

Exit Diskpart

exit


---

Installing Windows

> DO NOT USE Windows 11 24H2 Builds!!!!



Replace path\to\install.esd with the actual path of your Windows ARM image (either .esd or .wim):

dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\

If you encounter Error 87, check the correct index for Windows 11 Pro:

dism /get-imageinfo /ImageFile:path\to\install.esd

Replace index:6 with the correct index.


---

Installing Drivers

Extract the drivers and add them:

dism /image:X:\ /add-driver /driver:path\to\drivers /recurse


---

Creating the Bootloader

Create bootloader files:

bcdboot X:\Windows /s Y: /f UEFI


---

Configuring the Bootloader

Enable test signing:

bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on

Disable recovery:

bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no

Disable integrity checks:

bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on


---

Clean Up ESP Drive Letter

If possible, remove the drive letter for the ESP partition:

mountvol y: /d

If it doesn’t work, the phantom drive will disappear on the next reboot.


---

Reboot to Android

Reboot the device to set up dual boot.


---

Final Step: Setting up Dual Boot

Follow the steps outlined in the dualboot.md guide to finalize the dual boot setup.
