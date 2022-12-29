---
title: WebUSB
---
WebUSB is a standard that lets browsers talk to USB devices directly. ProffieOS uses this to let you control and configure the board from a browser. To make WebUSB work, you need:

1. A Proffieboard, WebUSB currently does not work with Teensys connected via USB, it does work for both Teensy and Proffieboard via BLE connection.
2. ProffieOS 1.312 or later
3. 0.1.7 or later of the [proffieboard-arduino](https://github.com/profezzorn/arduino-proffieboard) plugin.
4. A browser that supports WebUSB, such as Chrome. see here for more information: https://caniuse.com/webusb
5. A USB cable (not charge-only!), or BLE connection.

Depending on how you want to connect the WebUSB app to your saber make sure to set the configuration for the serial port as follows;
Proffieboard connected via USB to WebUSB app;
- Select :  USB type: "Serial + WebUSB" in the Arduino IDE, or "Serial + Mass Storage + WebUSB if you also want to access the SD card without removing it
-Teensy based sabers connected via USB to the WebUSB app are not yet supported.

Proffieboard or Teensysaber connected via BLE to WebUSB app;
- Make sure #define ENABLE_SERIAL is in your config file, and your Bluetooth device is working. 
- USB type : "Serial" will work for both Teensy and Proffieboard

After that, plug in the board to a computer or phone if you want to use the USB connection, or connect via BLE from within a webpage that can control the board, such as: https://profezzorn.github.io/lightsaber-web-bluetooth/app.html

### Troubleshooting

ProffieOS has some code that allows Windows 8.1+ assign the right driver automatically to make WebUSB work.
Unfortunately, that code does not work with Windows 7. so if you're using Windows 7 you have to use zadig to make WebUSB work:

* Run [Zadig](zadig.html)
* Select Options->List All Devices
* Select "CDC Data (interface 2)"
* Check that the USB ID is 1209 6668 02
* Select WinUSB (v6.1.7600.16385) as new driver
* Click Replace Driver

If you're having problems with making WebUSB work on Windows 10, it may be because of having used zadig to override the windows defaults for the proffieboard device. If so, this is how you undo zadig overrides: https://github.com/pbatard/libwdi/wiki/FAQ#Help_Zadig_replaced_the_driver_for_the_wrong_device_How_do_I_restore_it

The WebUSB app will work on Windows, Linux and Android, but to get BLE working on IOS, you might need to install a WebBLE enabled browser on you IOS device (chrome for IOS does not suppert WebBLE yet). 

Update 2022-06: Bluefy (free) from the appstore used to work perfect with the WebUSB app. Unfortunately that is no longer the case as of beginning of 2021. 

An alternative for IOS users is the WebBLE app, and has been tested with the latest IOS version. https://apps.apple.com/us/app/webble/id1193531073


Here's a tutorial for how to get around the ProffieOS Workbench webpage:  
https://fredrik.hubbe.net/lightsaber/webusb.html