---
title: ProffieOS v6.x, Keeping edits when uploading
redirect_from:
  - /proffieos6-keeping-edits-when-uploading.html
---
In ProffieOS6, all edits made to your presets or settings in either [Edit Mode](https://fett263.s3.us-east-2.amazonaws.com/proffieOS6-edit-mode.html) or using [ProffieOS Workbench (WebUSB)](/webusb.html) are saved to your SD card in various *.ini files.  
NOTE: It is strongly recommended you save a backup of all SD card contents (fonts and *.ini files) after making edits in case your SD card is erased or corrupted.

Typically, whenever you reupload through Arduino the existing .ini files are ignored.  In order to prevent this you will want to include this define in your config BEFORE you make your edits.

`#define KEEP_SAVEFILES_WHEN_PROGRAMMING`

This define will allow you to keep all previous Edits (so long as the .ini files were not erased or overwritten). As such this define is intended to be used when you no longer wish to upload changes via Arduino and only edit the saber via Edit Mode or ProffieOS Workbench.

### However, BEFORE USING THIS DEFINE it's important to note the following.  

#1 With #define KEEP_SAVEFILES_WHEN_PROGRAMMING changes to fonts, tracks, colors/settings, control defines (i.e. gestures) as well as volume, blade length and clash threshold in the config you upload will not be used, instead the saber will continue to use any previous values that exist in the .ini files.
This means that if you're trying to make changes or adjustments via uploading changes to the config those changes may not actually appear on your saber after the upload if there are different values in the related .ini.  So if you have a specific clash threshold or a font already in a .ini file the new value you put into your config and uploaded would not appear so you would then use Edit Mode or ProffieOS Workbench to make your adjustments.
For this reason, it is not recommended that you add this define until you have the baseline for your saber set for the following:
* clash_threshold (CLASH_THRESHOLD_G)
* max volume (VOLUME) 
* max blade length (set in BladeConfig for each blade)
* all desired styles (see below)
* other starting settings such as swing on speed, lockup delay, clash detect, max clash, brightness
Once you have the saber set up in the form and with all styles that you want you would then add the above define to allow for all future adjustments and edits to made using Edit Mode or ProffieOS Workbench as intended.

#2a The style number in presets.ini is based on the order of the styles in the recently uploaded config beginning with 0.  So all styles in the first preset of your config are equal to "style number 0".  So if you change style code in a preset all presets that were edited to use "style number 0" will reflect the new style from the most recently uploaded config.  
If this is not desired it is recommended you add new style code to a new preset at the end of the config and use an editing method to change on the desired presets.

#2b Related to above if you add a new preset to your config and upload it will not be visible on the saber until you use Edit Mode or ProffieOS Workbench to Copy Preset (add a preset) and then select the new style number and set up the font and track.  This is because presets.ini will not have a reference to new presets uploaded.  The style code from your new presets is stored on the board (if upload is successful) but there won't be any presets in the .ini that utilize. 
The easiest way to get the new style into a preset is to use Copy Preset for an existing preset, then Edit the style number to use the new style code and change Font and Track as desired.

#3 **You should not remove presets from your config**.  
Because presets.ini is not updated on upload with this define if you upload a config missing a style number that is referenced it will cause the board to lock up.  So if your original config had 15 presets and you upload a config that removes a preset presets.ini will reference style number 14 but it will not exist on the board.  
The simplest approach would be to replace the style for that preset in your config if you no longer wish to use that specific style code (see #2a above).
If you only wish to not have the preset on your saber but don't need to remove the style code, just select the preset and use the Delete Preset functionality in Edit Mode or ProffieOS Workbench.
If it's absolutely necessary to remove the style entirely then you will need to manually update your presets.ini file to change all instances of the style number(s) removed keeping in mind they are always sequential from the first preset starting at 0 to the final preset (being equal to preset # - 1).  So if you have 15 presets the final style number is "14".  If you delete the last preset in your config and upload (without replacing) you would need to manually change any preset the uses:

`style=builtin 14 1`

and change the "14" to any number between 0 and 13 corresponding to the style you want.  See [Edit presets.ini by Hand](/howto/editing-presets.ini-by-hand.html) for more information.

Once you have all of the initial settings and the styles you want uploaded to your saber you can then use this define to move all edits to Edit Mode or ProffieOS Workbench.
