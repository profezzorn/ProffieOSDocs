# Arduino Plugin for [Proffieboard](https://fredrik.hubbe.net/lightsaber/v4/)

## Installing

 1. [Download and install the Arduino IDE](https://www.arduino.cc/en/software) (version v1.6.19 or later)
 2. Start the Arduino IDE
 3. Go into Preferences
 4. Add ```https://profezzorn.github.io/arduino-proffieboard/package_proffieboard_index.json``` as an "Additional Board Manager URL"
 5. Open Arduino menu Tools->Board->Boards Manager and type "Proffie" in the search box. Install the latest version "Proffieboard Plugin"
 6. Select your board version from Arduino menu Tools->Board->Proffieboard-> menu 
 7. Set Tools->DOSFS: to "SDCARD (SPI)".  For Proffieboard V3, choose "SDCARD (SDIO High Speed)" 

### OS Specific Setup

####  Windows

##### STM32 BOOTLOADER driver setup for STM32L4 based boards

 1. Download [Zadig](https://zadig.akeo.ie/)
 2. Plugin the Proffieboard and check Arduino menu Tools->Port for a COM or that says (Proffieboard).
- If it's there, open Tools->Serial Monitor and type ```RebootDFU``` and hit return (or click the "Send" button).
- If it's NOT there, you'll need to use the onboard buttons. Press and hold BOOT, press and release RESET, then release BOOT.
 3. Let Windows finish searching for drivers
 4. Start ```Zadig```
 5. Select ```Options -> List All Devices```
 6. Select ```STM32 BOOTLOADER``` from the device dropdown
 7. Verify that the USB ID is ```0483 df11```, if it is not, do not proceed!
 8. Select ```WinUSB (v6.1.7600.16385)``` as new driver 
 9. Click ```Install Driver``` or ```Replace Driver```
10. At this point, you can either do step 11 below, or:
- just hit upload in Arduino with a known good config file declared (default_proffieboard_config.h is a good choice) even though the board does not show up on Arduino menu Tools>Port (it's still in Bootloader mode).
- After upload is successful (1-100% progress bar and "done uploading" showing) the board should appear under Tools->Port as (Proffieboard).
11. Power off the board by unplugging USB and killing battery power. When reconnected, the board should appear under Tools->Port as (Proffieboard).
##### USB Serial driver setup for STM32L4 based boards (Windows 7/XP only, not for Windows 8 or 10)

 1. Go to ~/AppData/Local/Arduino15/packages/profezzorn/hardware/stm32l4/```<VERSION>```/drivers/windows
 2. Right-click on ```dpinst_x86.exe``` (32 bit Windows) or ```dpinst_amd64.exe``` (64 bit Windows) and select ```Run as administrator```
 3. Click on ```Install this driver software anyway``` at the ```Windows Security``` popup as the driver is unsigned

#### Linux

 1. Go to ~/.arduino15/packages/profezzorn/hardware/stm32l4/```<VERSION>```/drivers/linux/
 2. sudo cp *.rules /etc/udev/rules.d
 3. reboot

## Troubleshooting

### How do I know if uploads are working?

 Look at the bottom secton of the arduino program. The progress of the upload will show in red text. Unfortunately arduino will not scroll down automatically as uploads are taking place, so if you want to see how it's doing you have to  keep scrolling down while it's working.

### Recovering from a broken upload

 Sometimes a faulty sketch can render the normal USB Serial based integration into the Arduindo IDE not working. In this case plugin the Proffieboard and toggle the RESET button while holding down the BOOT button and program a known to be working sketch to go ack to a working USB Serial setup.

### Connection issues

#### Windows 10
 Go to the control panel and click on Bluetooth & other devices. It should either show "Proffieboard" or "STM32 BOOTLOADER". If you hold BOOT and click RESET, it should show "STM32 BOOTLOADER". If neither show up, try a different USB port or cable.

#### Linux
 Running ```sudo tail -f /var/log/kern.log``` will show you when things connect and disconnect, the lsusb command is also helpful.

