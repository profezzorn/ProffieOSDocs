If the Proffieboard Port doesn't show up in Arduino->Tools->Port, don't worry, most of the time you just need to press BOOT+RESET and hit upload. After the board is programmed, the port will show up again.

If programming works, but the port still doesn't show up, it's possible that you you need to install a driver.
If you're on a Mac, you may need to upgrade to a later version of OSX.
On linux, make sure you have the udev rules installed. See [Proffieboard Setup](../proffieboard-setup.md)
If you're on Windows 7, follow the usb serial driver instructions here: [Proffieboard Setup](../proffieboard-setup.md)
On Windows 10, it *should* just work.

If it still doesn't work, it's possible that some other software has messed things up, or perhaps you used zadig incorrectly and changed the driver for the Proffieboard serial device. Here is how you check what driver is used on Windows 10:

* Go to Settings->Devices
* Scroll down and click on "Devices and printers"
* In the "Unspecified" category, find "Proffieboard".  (If it's not there, go back and program the board first.)
* Double-click the proffieboard device.
* Select the "Hardware" tab.
* You should see a list of device functions, which should contain "USB Composite Device" and "USB Serial Device"
* Double-click the "USB Serial Device"
* Select the Driver tab
* Click "Driver Details"
* It should say "C:\WINDOWS\system32\DRIVERS\usbser.sys"

It's possible that usbser.sys lives in a different location, and that's probably fine.
However, if you see "winusb.sys" or some completely different driver, you probably ran zadig on the wrong device at some point. Here is how you undo it: https://github.com/pbatard/libwdi/wiki/FAQ#Help_Zadig_replaced_the_driver_for_the_wrong_device_How_do_I_restore_it

Here is a video that shows how to check and fix the serial port driver: https://www.youtube.com/watch?v=XgT8dq4rhPk
