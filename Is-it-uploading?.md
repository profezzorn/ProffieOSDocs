When you upload to a Proffieboard, the progress of the upload is shown in the same window as compile errors, in the bottom section of the Arduino program. There are a couple of stages, and each one can fail.  

If you have a Teensy, you should get a small pop-up window with a progress bar that moves as the program is uploaded.  

First, if a serial port attached to a Proffieboard is detected, it will signal the board to reboot into bootloader mode.  This doesn't always work properly, and the port may need to be configured manually in Tools->Port. Note that the correct port may say "butterfly" or "Proffieboard". Note that on Windows 7, a special driver is needed for the port to work. See: https://zadig.akeo.ie/

While the code is waiting for the board to reboot into bootloader mode, it will write out the numbers 1 to 10, once per second. If it gets to 10 without finding the bootloader it just gives up. If that happens, try these directions:

1. Connect Proffieboard to computer.
2. Hold the BOOT button.
3. Press and release the RESET button.
4. Check that the computer can see your board as STM32 BOOTLOADER. (See this page for how to find all USB devices connected to your computer: [USB Connection Issues](USB-Connection-Issues.md))
5. If the board was not recognized by your computer, try a different cable, port, computer, etc. Ultimately, if the board cannot be found, it may be broken.
6. Once the board is found, press the upload button in Arduino. Note that there will be no port listed under Arduino->Tools->Port, but if your board is already in bootloader mode, upload should work anyways.

Once the bootloader is found, it will start uploading, which will take ~30 seconds or so.
During the upload, progress bars will be printed.  What you should see is a bunch of lines that look like this:

`Download  [=======                            ]   30%        123128 bytes`

Once it gets to 100%, the board will reboot and your upload will have completed successfully.

If you get this message instead:
"cannot open dfu device 0483:df11", it means that it found the bootloader, but it can't talk to it. On windows, that usually means that you need to run [zadig](zadig.md) to install the right driver for the STM32 BOOTLOADER. On Linux, it means that you need to install the right udev rules.

If you get this message "Please select a Port before Upload", but there are no ports to choose from. Please try installing Arduino 1.8.6 or earlier.

See also: [USB Connection Issues](USB-Connection-Issues.md)
