---
title: How to back up a Proffieboard
---
If you want to backup the program that is currently on your Proffieboard, you can do so by going here:

   https://profezzorn.github.io/webdfu/dfu-util/

Connect your Proffieboard to your computer with USB and make it go into bootloader mode.  
The easiest way to do this is by issuing a command in Arduino's Serial Monitor, `RebootDFU`.  
The physical way requires accessing the Proffieboard onboard buttons. (Hold BOOT, press and release RESET, then release BOOT.)  
If you're running a Windows computer and this is the first time you are connecting a Proffieboard via USB, then you will also need to run [Zadig](../zadig.html).

Now click 'Connect' in the programmer. You should be prompted to connect to 'STM32  BOOTLOADER'.  
Click 'Read'.  This will save a .bin file to your computer that is a backup of the programming on the board.
A good idea might be to make a new folder to store your backups, something like:  
'/User.../lightsabers/backups/Graflex/' then name the download file 'Graflex_Nov11-2021.bin'.  
Note that this is not a config file and there isn't a way to tell how the board was configured from the downloaded file.

If you later want to restore this backed up programming to your Proffieboard, you can go back to the page listed above, connect again, then click 'Write' and select the file you previously downloaded. This will restore the programming to the way it was.

Note that some options may be stored on the SD card as .ini files, so you probably want to preserve those too.  
Simply copying them to your backup folder mentioned above would be ideal.