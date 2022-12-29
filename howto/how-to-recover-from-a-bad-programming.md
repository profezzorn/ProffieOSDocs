---
title: How to recover from a bad programming
---
If your ProffieBoard is unresponsive, either because of creating a program that doesn't work, or because of interrupting a programming in a middle. Don't worry here's what you need to do:

1. Plug in your Proffieboard to your computer
1. hold the BOOT button.
1. press and release the RESET button.
1. Make sure that the board shows up as "STM32 BOOTLOADER" on your computer. [Click here to learn how to check.](../troubleshooting/usb-connection-issues.html) If you don't see "STM32 BOOTLOADER" connected to your computer, try again. If you cannot get past this step, regardless of how many cables you try, then there is most likely something wrong with your board, or you're not actually pushing the buttons correctly.
1. Click the upload button in Arduino. Note that the board will not show up under "Arduino -> Tools -> Port". This is expected and not a problem, upload should work anyays.
1. If the upload [went well](../troubleshooting/is-it-uploading.html), your board should now be working normally.
