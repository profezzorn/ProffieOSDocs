---
title: Zadig
redirect_from:
  - /zadig.html
---

Zadig is a program that let's you update or replace device drivers for specific USB devices on Windows. For Proffieboards, we can Zadig to install a driver that lets us talk to the STM32 BOOTLOADER. However, it's easier to just use [proffie-dfu-setup.exe](https://fredrik.hubbe.net/lightsaber/proffie-dfu-setup.exe). If proffie-defu-setup.exe doesn't work, or you just prefer to do things the hard way, here is how you do it with Zadig:

 1. Download [Zadig](https://zadig.akeo.ie/)
 2. Plugin the Proffieboard and toggle the RESET button while holding down the BOOT button
 3. Let Windows finish searching for drivers
 4. Start ```Zadig```
 5. Select ```Options -> List All Devices```
 6. Select ```STM32 BOOTLOADER``` from the device dropdown
 7. **Verify that the USB ID is ```0483 df11```, if it is not, do not proceed!**
 8. Select ```WinUSB (v6.1.7600.16385)``` as new driver
 9. Click ```Replace Driver```

Done. Once zadig has been run, you shouldn't have to do it again. Your computer should remember
what driver to use for the proffieboard bootloader from now on.

Note that on Windows 7, you will probably also need to update the ACM serial device driver, but that is done with a separate program.

Zadig doesn't have an undo, or revert button, but if you run Zadig on the wrong device, here is how you revert it: https://github.com/pbatard/libwdi/wiki/FAQ#Help_Zadig_replaced_the_driver_for_the_wrong_device_How_do_I_restore_it
