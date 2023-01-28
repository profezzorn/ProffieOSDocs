---
title: Proffieboard Setup
---
This page will walk you through installing and configuring the software you need to program your Proffieboards. This includes installing Arduino, the arduino-proffieboard plugin, which provides Proffieboard support to Arduino, and any drivers you might need, which depends on what kind of computer you have.

## Arduino
Go to https://www.arduino.cc/en/software and download the Arduino IDE version v1.6.19 or later. Once downloaded, run it to install the Arduino software on your computer.

## The Arduino-Proffieboard plugin
 1. Start the Arduino IDE
 3. Go into File -> Preferences
 3. In "Additional Board Manager URL", enter the following:
```text
https://profezzorn.github.io/arduino-proffieboard/package_proffieboard_index.json
```    
It should look like this:
![arduino preferences](/images/arduino_preferences.png)

 6. Open Arduino menu Tools->Board->Boards Manager and type "Proffie" in the search box. Install the latest version "Proffieboard Plugin". You may have to click on it for the "install" button to appear. Once done, it should look like this:

![arduino board manager](/images/arduino_board_manager.png)

 8. Select your board version from Arduino menu Tools->Board->Proffieboard-> menu 
 9. Set Tools->DOSFS: to "SDCARD (SPI)".  For Proffieboard V3, choose "SDCARD (SDIO High Speed)" 

When you're done, the tools menu should look like this:
![arduino tools menu](/images/arduino_tools_menu.png)


## OS Specific Setup

###  Windows
Download [proffie-dfu-setup](https://fredrik.hubbe.net/lightsaber/proffie-dfu-setup.exe) and run it. (sha256: 4773c8693cf62777cd8da4c95441690e7ae7c4171e8c1d533b1f6225f3bdc29e)

If you're using Windows 7 or earlier, you also need to install a USB ACM serial driver:
 1. Go to ~/AppData/Local/Arduino15/packages/profezzorn/hardware/stm32l4/```<VERSION>```/drivers/windows
 2. Right-click on ```dpinst_x86.exe``` (32 bit Windows) or ```dpinst_amd64.exe``` (64 bit Windows) and select ```Run as administrator```
 3. Click on ```Install this driver software anyway``` at the ```Windows Security``` popup as the driver is unsigned

### Linux

 1. Go to ~/.arduino15/packages/profezzorn/hardware/stm32l4/```<VERSION>```/drivers/linux/
 2. sudo cp *.rules /etc/udev/rules.d
 3. reboot

### Mac
If you're using an M1/M2 mac, you're going to need to install Rosetta. The Arduino-Proffieboard plugin does not have native arm-mac support yet.

## Done

Now you're ready to configure, compile and upload ProffieOS to your Proffieboards.
