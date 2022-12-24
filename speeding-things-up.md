---
title: Speeding things up
---
Sometimes, ProffieOS will run slowly, because it has too many things to do and too little time to do it. Here is a list of possible things you can do about it.


### Use the "top" command to identify what is using up all the CPU time.

Note that "top" will not be available if you have `#define DISABLE_DIAGNOSTICS_COMMANDS` in your config file. Also note that "top" produces very different numbers when the saber is on and when it's off. Finally, top shows the cpu statistics since the last time you ran it, so generally you will want to turn the saber on, run "top", wait a few seconds, then run "top" again.

### Turn on optimization in Tools->Optimization

Lots of things gets faster when you turn on optimization. However, they also get bigger, so you may run out of flash memory. See the [Saving Memory](saving-memory.md) page for how to reduce flash memory usage.

### Use ProffieOS 5.x or later

ProffieOS 5.x has a better WS281X driver which is both faster and uses less RAM. In addition, if you set maxLedsPerStrip to a number a little higher than it needs to be, ProffieOS 5.x will be able to run styles and feed out data more effectively in parallel.

### Overclock pixel strips

While nearly all WS281X are specified to run at 800kHz, most of them can run faster than that, so you can get things to run a little faster and smoother by feeding out bits faster.  To do so, you would change a typical blade definition from:

     WS281XBladePtr<529, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>()

to:

     WS281XBladePtr<529, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>, DefaultPinClass, 1000000>()


### Speed up the SD card

A slow SD card can slow down ProffieOS a lot. So make sure that your SD card is fast enough. In addition, there are things you can do to make it easier for ProffieOS to find files on the SD card, which is a small, but helpful speedup:

 * Don't move files back-and-forth, rename and copy and do lots of operations on the SD card. These operations may grow the directory tables and make finding files takes longer. If you have done a lot of these sort of operations on your SD card, you might want to copy all the files from the SD card to your computer, format the SD card and copy the files back. After doing that, only the directory entries that are required will be on the SD card.
 * Don't have a lot of extra files in the font and root directories on the SD card. If you put them in a sub-directory, it is fine.
 * Don't put font deeply into the directory structure. If your font is in "fonts/obi/ep4/font11", it will take longer to open the files than if the font was simply called "obi11".
 * Don't use long filenames. Long filenames use up more directory entries and will make it take slightly longer to find *other* files in the same directory. However, making file names shorter than 8 characters, plus 3 characters for the extension has no effect on speed.
 * Prefer using the "EffectName/NNN.wav" structure over "EffectNameNNN.wav". Because of the way FAT32 works, having lots and lots of files in the same directory will make some of those files take longer to open. By creating sub-directories for each effect name (if that effect has more than one file) it will make finding files easier.

Finally, sometimes SD cards become slow as they get older. Doing the format-and-replace-all-the-files maneuver might fix such problems, but at some point, you may need to just replace the SD card even if it was working fine in the past.

