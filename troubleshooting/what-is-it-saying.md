---
title: What is it saying?
---
ProffieOS has several spoken error messages. While spoken error messages are meant to be user friendly, it can sometimes be difficult to hear what it's actually saying. Luckily, there is a fairly short list of actual error messages:

### Font directory not found
This happens when the font specified in your your current preset cannot be found on the SD card. A common reason for this is mispelling the font name in one of the 2 places; the SD card or the preset. They need to be identically spelled with no spaces preferably.  
It may also be a path problem. For example "Greyscale/CODA" is not the same as "CODA". The preset's font path must match the folder structure on the SD card.  
It could also be if "ProffieOS_SD_Card" sounds were downloaded and put incorrectly on the SD card. What you're supposed to do is to just copy the contents of that directory to the root level of the SD.

### Font directory too long - Teensysaber boards only as of ProffieOS 6.x.
If your font directory can't be found AND the name is longer than 8 characters, you may get this error message. Check the path and name of the font folder you specified in the preset and make sure it matched exactly on the SD card.

### SD card not found
This means that the board cannot detect the SD card. Either the SD card is not present, it's not formatted as FAT32, or something electrical is wrong.

### Error in font directory
This means that one or more sound effect files are missing or incorrectly numbered. For instance, if you have hum1.wav, hum2.wav and hum4.wav (but no hum3.wav) you will get this error message.

### Error in blade array
This happens if the blade array is not configured correctly.
The reasons may be complicated, so ask for help if you can't figure it out.

### Low battery
Charge it!

### Something else
If you hear it saying something else, this page may be out of date and will need to be updated, please remind me to do so.
