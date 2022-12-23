In order to be able to upload programs to a Proffieboard or Teensy, your computer must be able to talk to it.
While there are various drivers permission issues that may need to be solved, this page explains how to tell if he connection is working at all.

Most operating systems have a way to view all connected devices. When a Proffieboard is connected, it should show up as either a "Proffieboard" or "STM32 BOOTLOADER".  A bad program may lock the processor in a loop, preventing it from communicating with the computer, if that happens, press RESET while holding BOOT, and it should show up as "STM32 BOOTLOADER".

Here is how to check connected devices on...

## Windows 10

Go to Start Menu->Control Panel->Devices and Printers

## Windows 7

Go to Control Panel -> Devices and Printers

## Mac

Apple Menu -> About this Mac -> System Report -> USB

## Linux

Open up a shell and type "lsusb"


Now, if nothing shows up, try a different USB cable, as some micro-USB cables are charge-only.
If you need to buy a new cable, I recommend buying one that is USB-IF certified.


Once you have verified that the board shows up properly, proceed to [Where's my Port?](wheres-my-port.md).