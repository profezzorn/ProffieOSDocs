---
title: Navigating the menu system
---

ProffieOS has a configurable menu system which can be configured with any menus you want. Also, some props have their own menues. This page describes the default menues, which is what you get by using this define with a prop that supports it:

```cpp
#define MENU_SPEC_TEMPLATE DefaultMenuSpec
```

(Currently, this is supported by the default "saber" prop, and the "saber_BC_buttons" prop.)

The prop will have some button for entering the menu system, when using the default "saber" prop, this is by double-clicking the AUX button while the saber is off. Once you enter the menu system, these are your controls:

* Click POWER - select
* Click AUX - back / cancel
* Rotate hilt left/right around it's axis - go to the next / previous menu entry
* You can use "left", "right", "select" and "cancel" in the serial monitor to navigate the menues as well.

The saber will tell you what menu entry it's on through the speaker, so make sure to have a speaker connected when navigating the menu.

# The top menu
When you enter the menu system, this is where you end up. The default top menu has two entries, both of which leads to sub-menus:

* [Edit Presets](#theeditpresetsmenu)
* [Settings](#thesettingsmenu)

# The Settings Menu
The settings menu is fairly simple. Note that depending on what defines you use, some of these settings might not be available. Depending on your defines, these settings may be saved between reboots, or not.

* Change Volume
This allows you to change the volume. Select, rotate left / right to adjust the volume, then click power to select the volume you want. See also the [VOLUME_MENU_GAMMA](/config/the-config_top-section.html#volumemenugamma) define.

* SD Access
Lets you select if the SD card can be accessed from a computer or not. Defaults to off to protect the SD card from accidental corruption when programming the board. Available with the [MOUNT_SD_SETTING](/config/the-config_top-section.html#mountsdsetting) define.

* Blade Length
Lets you shorten the blade to match the inserted blade.

### Clash Threshold
Lets you adjust the clash threshold. Reasonable values range from around 1 to 8.

### Blade Dimming
Lets you make all your LEDs darker, can be helpful to save on battery, or when using your saber in a dark environment.

# The Edit Presets Menu

### Select Font
This will go to a sub-menu, where each entry is a font on your SD card. Note that all fonts must be in the top-level to be found, and must have a "font.wav" file so you know which font it is. If you click AUX, it will exit the menu without changing anything, if you click POW, the selected font will be used for the current preset.

### Select Track
Similar to the "Select Font" sub menu, but for tracks. Tracks must be in `/tracks/*.wav` or `/FONT/tracks/*.wav` to be found.

### [Edit Blade Style](#theeditbladestylemenu) (one per blade)
If you have multiple blades (or accents, illuminated PCBs, buttons, etc.) there will be multiple "Select blade style" menus, one per blade. Selecting this entry will enter the "Edit Blade Style" menu, see below.

### Move Preset Up
Moves the current preset up one step.

### Move Preset Down
Moves the current preset down one step.

### Select Preset
Selects the current preset for insertion.

### Insert Selected Preset
Inserts a copy of the selected preset before the current preset. It's recommended to immediately change the font for the new preset so that you can tell them apart.

### Delete Preset
This will enter a confirmation menu that has several cancel entries and one select entry. If you select the select entry, the current preset will be deleted. While the deleted entry can be reconstructed, there is no easy "undo", apart from deleting your presets.ini and presets.tmp files, which would reset all edits made using the menu system.

# The Edit Blade Style Menu
### (Edit Style Options)[#theeditstyleoptionsmenu]
If this style has options that can be changed, like base color, retraction time, etc. then selecting this will enter a menu which lets you change those options.

### Select Style Entry
Remembers the colors from this style entry, so that they can later be applied to another style, possibly in a completely different preset.

### Apply Colors From Selected Style Entry
Copies the colors from a previously selected entry to this style.

### Apply Colors To All Blades
Applies the colors of this style to all other styles in the same preset.

### Reset Colors
Resets all colors of this style to their defaults.

### Reset Style Options
Resets all colors, options and timing values for this style to their defaults.

### (Select Style)[#theselectstylemenu]
This will let you select a different style from any of the presets in the config file.

# The Edit Style Options Menu
Note that only those options that your style actually uses will show up in this menu, so while this menu is fairly long, it might not be when you access it on your saber. If you select a color option in this menu, it will go to [the color menu](#thecolormenu), if you select any other option, you will enter a menu that lets you select the value for that option.

### Base Color
### Alt Color
### Style Option
### Ignition Option
### Ignition Time
### Ignition Delay
### Ignition Color
### Ignition Power Up Option
### Blast Color
### Clash Color
### Lockup Color
### Lockup Position
### Drag Color
### Drag Size
### Lightning Block Color
### Stab Color
### Melt Color
### Swing Color
### Swing Option
### Emitter Color
### Emitter Size
### Preon Color
### Preon Option
### Preon Size
### Retraction Option
### Retraction Time
### Retraction Delay
### Retraction Color
### Retraction Cool Down Arg
### Postoff Color
### Off Color
### Alt Color 2
### Alt Color 3
### Style Option 2
### Style Option 3
### Ignition Option 2
### Retraction Option 2

# The Color Menu
This menu lets you make changes to a single color. The color will be showing on all blades while you are in this menu. You need to select the "Save" entry at the end for anything to change. If you just exit the menu by pressing AUX, your changes will not be saved.

### Color List (select color by name)
This lets you select a color by name. The list of available names might depend on what voice pack you choose.

### Change Color by Hue
This lets you chage the hue of the current color using a color wheel, similar to the "color change mode".

### Change Color Brightness
Lets you make the current color lighter or darker, please remember that making it too bright will desaturate the color and make it less colorful.

### Change Red
Lets you change the red value.

### Change Green
Lets you change the green value.

### Change Blue
Lets you change the blue value.

### Select Color
Remembers the current color.

### Use Selected Color
Recalls the remembered color from the prevoius menu entry.

### Reset Color to Default
Resets the color to the default as specified by the style.

### Save
Please remember to select this after changing the color, or the change will not be saved.
