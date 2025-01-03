# Running Windows on the Redmi Note 13 Pro

## Root guide

### Prerequisites
- [Magisk](https://github.com/topjohnwu/Magisk/releases/latest)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Orange Fox](https://orangefox.download/device/garnet)

##### Boot Orange Fox
> If your recovery has been replaced back to stock, flash it again in fastboot with:
```cmd
fastboot flash recovery path\to\orangefox.img reboot recovery
```
##### Backing up your boot image
> Sometimes flashing Magisk can cause a bootloop. To fix this, you'll need to restore a boot.img backup.

Use the Orange Fox backup feature to make a backup of the boot partition.

##### Flashing Magisk
- Flash the magisk.apk (you may have to rename it to magisk.zip) and reboot your phone. 
- Once booted, locate the Magisk app and open it.
- Follow any instructions provided. Select the direct install method if you are provided with several methods.

Your phone will now reboot, and you have succesfully rooted it.

> [!IMPORTANT]
> After you've rooted your phone, create a new boot.img backup in Android and in Windows (using the WOA Helper app) and remove any remaining boot.img backups you have made previously. If you don't do this, switching to Android will unroot your phone.
> 
> After updating or changing your rom (and rerooting) you will have to repeat all the steps on this page.

## Finished!
