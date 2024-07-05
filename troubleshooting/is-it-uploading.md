---
title: Is it uploading?
---
When you upload to a Proffieboard, the progress of the upload is shown in the same window as compile errors, and it should look something like this:

<image src="/troubleshooting/images/successful_upload.png" width=686 height=531 alt="successful upload" />

Note that for some version of Arduino you will need to scroll down to see this. If you do not see this, or something similar, then the upload was probably not successful.


## Wrong port

One of the most common reasons for a failed upload is not selecting the right port. Usually this looks like this:

<image src="/troubleshooting/images/wrong_port.png" width=707 height=361 alt="wrong port" />

If this is what you see, select the right port in Arduino -> Tools -> Port, then try again. If the port is not shown, you can try these steps:

1. Connect Proffieboard to computer.
2. Hold the BOOT button.
3. Press and release the RESET button.
4. Check that the computer can see your board as STM32 BOOTLOADER. (See this page for how to find all USB devices connected to your computer: [USB Connection Issues](/troubleshooting/usb-connection-issues.html))
5. If the board was not recognized by your computer, try a different cable, port, computer, etc. Ultimately, if the board cannot be found, it may be broken.
6. Once the board is found, press the upload button in Arduino. Note that there will be no port listed under Arduino->Tools->Port, but if your board is already in bootloader mode, upload should work anyways.

Once upload has finished, the Port should be available in arduino, so you shouldn't have to do this process again.

## DFU driver not installed

<image src="/troubleshooting/images/cannot_open_dfu.png" width=699 height=513 alt="cannot open DFU device" />


If you get this message while uploading "cannot open dfu device 0483:df11", it means that it found the bootloader, but it can't talk to it.

On windows, that usually means that you need to run [proffie-dfu-setup](/tools/zadig.html) to install the right driver for the STM32 BOOTLOADER. On Linux, it means that you need to install the right udev rules.


If you see some other errors when uploading, it's probably a compile error. Check the [Arduino error messages](/troubleshooting/arduino-error-messages.html) page for help with those.

