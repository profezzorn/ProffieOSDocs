---
title: Saving FLASH Memory
redirect_from:
  - /saving-memory.html
---
If you see this when trying to compile ProffieOS

    `.text' will not fit in region `FLASH'

Then the combination of all the features and styles takes up too much space to fit on the board. Here is a list of things you can try to make it fit:

### Update to the latest available Arduino Proffieboard plug-in
Arduino menu Tools>Board>Boards Manager, type "proffie" in the search box. Install or update to the latest version available in the dropdown menu. Specifically, 3.6.0 introduced a lot of optimizations to save compiled code size.

### Use "smallest size"
In the Arduino menu Tools->Optimize, you can select "smallest size". This will disable some optimizations that usually make the compiled code bigger. The program will run a little slower, but that is generally not a problem.

### Don't use the POV style.
The POV style uses a lot of memory, and most people never really use it. Look for "&pov_style" in your config file and either replace those styles with something else, or remove the preset completely.

### Disable diagnostic commands
ProffieOS contains several serial monitor commands which are very useful for diagnosing problems, like "top", "monitor" and "dir". However, disabling these commands can save some memory. To do so you can add

    #define DISABLE_DIAGNOSTIC_COMMANDS

to your config file. Note that this define is only available in ProffieOS 3.x and over.

### Reduce number of presets, or use simpler styles.
If all else fails, you'll need to reduce the number of presets you use, or use less complicated blade styles.

### Use the same, or similar style for multiple presets
Using the same style multiple times in your config file uses no extra memory. This means that you can have multiple presets, with different fonts and tracks, but with identical blade styles, and it will use very little memory. Since ProffieOS 4.x, this short of memory saving also applies when making minor changes, like changing the base color of a blade. Basically: Having similar blade styles, but with different colors uses less memory than having unique blade styles for each preset.

### Disable basic parser styles  (ProffieOS 6.x or newer)
ProffieOS contains a few simple blade styles can be selected, used and customized from the ProffieOS Workbench by using Bluetooth or WebUSB.  If you never use the ProffieOS Workbench, you don't need these styles. Also, if you use styles updated for Edit Mode, then you will have lots of options for customization in the Workbench even if you don't have these basic styles. To disable them, you can add

    #define DISABLE_BASIC_PARSER_STYLES

to your config file.

### Use ProffieOS Workbench webpage, Edit Mode, or edit presets.ini by hand to add more presets.
Additional presets can be added to the saber by re-using existing code from the config file that was uploaded.
This will use no additional FLASH memory.  
This is done by instructing the OS to use an existing preset's blade style in a new preset, assigning any font, and even changing the color of the blade for that new preset. More information can be found at these links:  
https://fredrik.hubbe.net/lightsaber/webusb.html  
https://www.fett263.com/proffieOS6-edit-mode.html  
[Editing presets.ini by hand](/howto/editing-presets.ini-by-hand.html)

