---
title: How to install a new sound font
---
# Copying the font to the SD card.

First thing we need to do is to make the SD card show up on the computer. There are two ways to do this: Either we can take the SD card out of the saber and put it in an SD card reader attached to the computer, or if your saber is configured with the "mass storage" option, then you can use the Proffieboard as an SD card reader and just connect the saber to the computer with an USB cable. SD card readers are faster, but can be impractical if it's hard to get the SD card out of your saber.

Now, once the SD card shows up on the computer, we can put the font on it. Usually, what we want to do is to unzip the font into a new directory on your desktop, then copy or move that directory to the SD card. If the directory name is long, complicated or has weird characters in it, I suggest renaming it to something simple, preferably with only 8 characters. Sometimes font zip files contains a bunch of directories, and only one of those is intended to be used with ProffieOS, in which case you should only copy that directory to the SD card, not the whole thing.

Once it's copied, you should have a new directory in the top level directory of the SD card. That directory should contain the sounds and config files that make up the font. Although each of the sounds may be in a sub-directory in the font directory.

Now make sure to eject the sd card safely from the computer.

# Telling ProffieOS about the new font.

There are several ways to do that:
1. Use ProffieOS Workbench
2. Use Edit Mode
3. Add or change a preset and re-program the saber.
4. Edit presets.ini on the sd card.
5. Replace an existing font on SD card.

## Use ProffieOS Workbench.

I already wrote a guide for how to do this: https://fredrik.hubbe.net/lightsaber/webusb.html

## Use Edit Mode

If you have ProffieOS 6.x or later, and are using the Fett263 prop with edit mode enabled, then you can create and modify presets using the edit mode menu. For more information, go here: https://www.fett263.com/proffieOS6-intro.html

## Add or change a preset and re-program the saber.

See [the CONFIG_PRESETS section](/config/the-config_presets-section.html) for how to edit configure presets, then just follow the instructions for how to install ProffieOS to re-program the saber. Note that this can be tricky if you don't have the config file that was used to program the saber last time.

## Edit presets.ini directly

Using the ProffieOS workbench, or edit mode both ends up modifying a file on the sd card called presets.ini. This file can also be edited directly. I wouldn't normally recommend doing this, but if you want to, there is more information about how to do it here: [Editing presets.ini by hand](/config/editing-presets.ini-by-hand.html)

## Replacing an existing font on the SD card.

Some people find it easier to just name their font directories something generic, like "font1", "font2", etc. Then you can just replace the contents of those directories to switch the font sounds, and then ProffieOS doesn't need to be told how to find the sounds since they the sounds are in the same place, just new sounds. Of course, you could do this even if the directories aren't generically named, but it might be confusing to have a "darthvader" directory with a Luke font in it.
