# Running Windows on the Xiaomi Redmi Note 13 Pro 5G

## Partitioning Your Device

### Prerequisites
- A functional brain (most critical!)
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)  
- [Orange Fox Recovery](https://orangefox.download/device/garnet) (preferred)
- [Parted binary file]() (download soon).

---

### Important Notes
> ⚠️ **Warning:**  
> 
> - **Do NOT reboot your device** during any of these steps. If an issue arises, seek assistance in the [Telegram chat](https://t.me/joinchat/MNjTmBqHIokjweeN0SpoyA).  
> - Execute commands sequentially; running all at once may damage your device.
> - Missteps can lead to **permanent damage** to your phone.

---

### Opening CMD as an Administrator
1. Download **platform-tools** and extract it to a folder.  
2. Open CMD as an administrator.  
3. Navigate to the platform-tools folder:  
   ```cmd
   cd path\to\platform-tools


---

Flash Orange Fox Recovery (Preferred)

1. Boot the device into fastboot mode.


2. Flash recovery with this command:

fastboot flash recovery path\to\orangefox.img
fastboot reboot recovery




---

Backing Up Important Files

1. Back up fsg, fsc, modemst1, and modemst2:

cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"


2. Ensure the files are saved in the CMD's current path.




---

Partitioning Guide

This guide is optimized for the Redmi Note 13 Pro 5G, which comes in various storage sizes (128GB, 256GB, and 512GB). Adjust values for your specific device:

Unmount Data Partition

adb shell umount /dev/block/by-name/userdata

Push and Execute Parted

1. Download the parted binary file and place it in the platform-tools folder.


2. Run the following:

adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda



Print the Current Partition Table

1. To view all partitions:

print



Remove Userdata Partition

1. Replace $ with the number of the userdata partition (likely 21):

rm $



Recreate Userdata Partition

1. Replace 1611MB with the starting value and the end value based on your model's storage size:

mkpart userdata ext4 1611MB 32GB



Create ESP Partition

1. Replace 32GB with the end of the userdata partition and 32.3GB with userdata_end + 0.3GB:

mkpart esp fat32 32GB 32.3GB



Create Windows Partition

1. Replace 32.3GB with the ESP end value and adjust the disk end value based on your model:

mkpart win ntfs 32.3GB 123GB



Make ESP Partition Bootable

1. Use print to find the ESP partition number (likely 23):

set $ esp on



Exit Parted

quit


---

Formatting Drives

Format Windows Partition

1. Label it as WINDEVICE:

adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINDEVICE



Format ESP Partition

1. Label it as ESPGARNET:

adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPGARNET




---

Final Steps

Format all data in Orange Fox or TWRP to ensure Android boots:

Go to Wipe > Format Data > Type yes.


Restart the phone and confirm Android still works.



---

Next Step

Proceed to the Installing Windows Guide.
(https://github.com/maydoxx1/woa-garnet/blob/main/guide/2-install.md)


