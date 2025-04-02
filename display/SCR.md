---
title: SCR files
---

SCR files tells displays what to do. When event happens, the corresponding SCR files is read, and the instructions within are relayed to the display. SCR files are named in the same way as sound files, the only difference is that they are normally in a sub-directory called which is called 160x80, or whatever the resolution of your display is. Since displays can have multiple layers, an SCR file can have multiple sets of instructions, each separated by having "layer" on a single line.

# The instructions

### file=filename.pqf
This instruction tells the display to start playing "filename.pqf". The filename can be anything you want to. Note that if you have several PQF files and you want ProffieOS to choose one randomly, you must also have multiple SCR files, one for each PQF file. File names are relative to where the SCR files are, so if your SCR file is called "smthjedi/160x80/clash.scr" and your PQF file is called "smthjedi/160x80/pqf/clash.pqf", then you would use "file=pqf/clash.pqf". (No need to include the smthjedi/160x80 part.)

Note that if the layer is already playing this file, it will just continue playing it.

There should be at most one "file=..." per layer in an SCR file. If there is no "file=..." for a layer, it will just continue doign what it's doing.

### restart
The "restart" keyword doesn't do anything by itself. However, if there is a "file=..." in the same layer, and, it was already playing that file, then instead of just continuing, it will start from the beginning of the file.

### time=NNN
Non-animated and looped files will normally play forever, or until some other event occurs. This statement lets you put a time limit on how long the PQF will be playing. This also works for non-looped animations, but might not be needed since they will end naturally when the file runs out. The "NNN" part simply specifies how many milliseconds to play for.

### time=from_sound
This special form of the "time" assignment will take the time from the length of whatever WAV file was triggered by the same event. This does not make sense for SCR files that are not triggered by an event, like "on.scr" and "idle.scr".

### A, B, C, D, E = battery, volume, sound_level
These variable assignments actually look like this:
Examples:
```ini
A=battery
B=volume
C=sound_level
```

PQF files can have conditions based on variable values, and this is how you specify what those variables do. There are five possible variables: A through E, and two possible sources of values "battery" and "volume". Each value is converted to a 0-100 scale and fed to the PQF in real time.  More variable sources will be available in the future. By having these variables assigned here, you could create animations that show numbers, gauges or sound meters, and then decide afterwards if you want to use that animation to show the battery level, volume, or sound level.

# Examples
This is an example of boot.scr from a virtual crystal chamber animation setup:
```
file=vc.pqf
layer
file=batt.pqf
A=battery
layer
file=logo.pqf
```

* So, the first layer starts to play "vc.pqf". None of the other SCR files ever change this, so it just keeps playing forever.
* The second layer plays "batt.pqf", which has a battery level overlay in the bottom corner. Again, this never changes in any of the other SCR files.
* A=battery specifies that the "A" value (which is used by batt.pqf) will draw it's values from the battery sensor.
* The third layer will play logo.pqf, which shows "ProffieOS" for a few seconds, then becomes transparent, and then stops, which shows the layers below.

The "vc.pqf" file in this virtual crystal example has internal conditions that handles on/off, clash and lockup, so there is no need for the SCR files to do anything about that. For more information about PQF files, read [the PQF Page](/display/PQF.html).
