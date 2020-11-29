# ArgonONE M.2 Pi 4 Case Support for Home Assistant

The ArgonONE M.2 Pi 4 case is a great variant of the popular ArgonONE Pi 4 case, just with the addition of an M.2 SATA slot within the base of the case.  Utilizing Home Assistant while booting direct from the SSD requires the use of the Home Assistant OS 5.5 development track or greater (as of 29-11-2020).  After imaging the M.2 with HAOS, modify the drive using the instructions below.  After you have HAOS up and running you will then want to install Misiu's Argon40 fan integration.

ArgonONE M.2 Pi 4 case: https://www.argon40.com/argon-one-m-2-case-for-raspberry-pi-4.html
Misiu Argon40 fan integration: https://github.com/Misiu/argon40


# Instructions

1. Remove the USB port bridge and attach a USB cable between the storage port of the Argon40 case and another system running Linux.
2. Mount the first partition (the FAT partition), in my case it was /dev/sdb1.
3. Edit the config.txt using either nano or vi, adding the following lines.

     dtparam=i2c_vc=on
     
     dtparam=i2c_dev=on

4. (Optional) If you want to disable Wifi or Bluetooth while you're here, add the following lines under the [all] header.

     dtoverlay=disable-wifi
     
     dtoverlay=disable-bt

5. Create a directory titled CONFIG on the root of the drive.
6. Create a subdirectory under CONFIG called modules.
7. Create a file within the modules directory called rpi-i2c.conf with the contents of the two lines below.

     i2c-dev
     
     i2c-bcm2835

8. Unmount the drive and reinstall the USB port bridge.
9. Boot the Pi and wait until everything is back up then reboot again to make sure the changes are activated.
10. Install Misiu's Argon40 fan integration from https://github.com/Misiu/argon40.


# Notes

A) Some posts indicate you also need to add the line "i2c-bcm2708" as well in step seven above (below the other two lines).  However, I didn't need to do this.  If you have difficulty, you might try adding that line.

B) When you create the CONFIG and modules folders as well as the conf file below, after you successfully boot up it is normal for these files to be deleted.  HA removes them once they have been imported into your HA configuration.
