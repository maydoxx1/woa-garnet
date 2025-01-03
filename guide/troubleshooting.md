# Running Windows on the Redmi Note 13 Pro

## Troubleshooting Issues
> Below is a list of common problems and their solutions.

---

### **LTE and Other Network Services in Android No Longer Work**
> Windows may wipe modem partitions, causing LTE and network services to fail in Android. You need to restore your modem from backups.

#### Steps to Restore Modem:
1. Boot into any custom recovery (e.g., TWRP). Avoid stock recovery as ADB commands do not work there.
2. Open CMD in your **platform-tools** folder.
3. Restore the modem partitions using the following commands. Replace `path\to` with the actual backup file paths:

```cmd
adb shell dd if=path\to\fsc.bin of=/dev/block/by-name/fsc
adb shell dd if=path\to\fsg.bin of=/dev/block/by-name/fsg
adb shell dd if=path\to\modemst1.bin of=/dev/block/by-name/modemst1
adb shell dd if=path\to\modemst2.bin of=/dev/block/by-name/modemst2

4. Reboot your device and check LTE functionality.



> Note: If LTE still does not work:



Download the stock ROM for your device.

Extract the modem.img file from the ROM.

Boot into fastboot mode:


adb reboot bootloader

Flash the modem image:


fastboot flash modem path\to\modem.img

Finished!


---

Cannot Mount Windows in Android

> If mounting Windows produces an empty folder, either:



Windows is not installed.

Your Android ROM does not support Windows mounting.


Finished!


---

Cannot Write to Windows in Android

> Writing issues occur when Windows shuts down instead of restarting.



Solutions:

1. Boot into Windows, then select "Restart". As the screen turns off, boot into TWRP and load Android.


2. Alternatively, disable hibernation in Windows:

Open CMD as an administrator in Windows and run:


powercfg -h off



> If you've set up the Switch to Android app, use it to boot Android instead.



Finished!


---

USB Does Not Work

Enable USB host mode using the optional post-install guide.

Finished!


---

DISM Error: 87 - The add-driver Option is Unknown

> This occurs if you use an unclean Windows image with extra drivers.



Solution:

Obtain a clean Windows ARM image and redeploy.


Finished!


---

0xC000021A BSOD

> This BSOD indicates a failure in winlogon.exe.



Solution:

Reapply the Windows image using the deployment guide.


Finished!


---

The Computer Restarted Unexpectedly or Encountered an Unexpected Error

> This error means the deployment process failed.



Solution:

Redeploy the Windows image using the reinstall guide.


Finished!


---

INACCESSIBLE_BOOT_DEVICE BSOD

> This BSOD occurs due to broken driver installations.



Solution:

Reinstall the drivers using the reinstall guide.


Finished!


---
