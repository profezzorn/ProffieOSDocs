---
title: How to edit presets.ini by hand
---
Ok folks, so here is how you can use the ini files stored on the SD card to update your installed fonts and blade presets.

IMPORTANT: to use presets.ini, you have to flash the saber with the #define SAVE_PRESET in your config file, so the saber writes the preset information to the SD card. This define is blanketed under SAVE_STATE. ( See [The CONFIG_TOP Section](../config/the-config_top-section.md) )

First, open your presets.ini on the SD card using a text editor like Notepad ++ on PC or Textedit on Mac. It has a very basic structure:

First line is the 'installed date,' which is when the saber was last programmed
Then we have blocks of statements that look like this:

    new_preset
    font=TFAFlex
    track=tracks/rey_training.wav
    style=builtin 0 1
    style=builtin 0 2
    name=Graflex8
    variation=23299

That block of statements describes a preset. It shows the font, the track, blade style(s) (in this case, the saber in question has two 'blades:' the main blade an a pixel chamber), the name of the preset (used for OLED displays) and the 'variation' which is used for color-change. You'll see that the style entries show 'builtin and then two numbers. The first number corresponds to the first entry in your presets list and the second is which blade style in that entry should be used.

So for this saber, the config file entry for this preset looks like this:

    { "TFAFlex", "tracks/rey_training.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    StyleNormalPtr<Blue, WHITE, 300, 800>(), "Graflex8"},

So you can see how the config file entry matches what we see in the presets.ini style statements: builtin style, entry 0 (the first entry) and blade style 1 / 2

You will see several of these blocks, corresponding to the number of presets in your config file. At the end of the file, there is a single line with the word `end` which tells the saber that there are no more presets to use.

Now, if you want to alter your presets, you can change any of the lines in the block that describe a preset AND you can add new blocks. Here's how we would change this preset to use a new font:

    new_preset
    font=GraflexIV
    track=tracks/rey_training.wav
    style=builtin 0 1
    style=builtin 0 2
    name=Graflex8
    variation=23299

You could also change the track:

    new_preset
    font=GraflexIV
    track=tracks/rots.wav
    style=builtin 0 1
    style=builtin 0 2
    name=Graflex8
    variation=23299

Or even alter the styles to use entries from an entirely different preset:

    new_preset
    font=GraflexIV
    track=tracks/rots.wav
    style=builtin 3 1
    style=builtin 3 2
    name=Graflex8
    variation=23299

You could even use a blade style from one preset and a crystal chamber style from an entirely different preset:

    new_preset
    font=GraflexIV
    track=tracks/rots.wav
    style=builtin 3 1
    style=builtin 5 2
    name=Graflex8
    variation=23299

So as you can see, the presets.ini can be modified by editing a couple lines and totally change how that preset functions when the saber is used. You can also insert as many preset blocks as you like, so long as they reference the blade styles in your config file and there is a single line at the end of presets.ini with the word `end` to tell the saber that the list of presets is finished.

For anyone struggling with 'running out of memory' or if you want to tinker with the saber without reflashing, take a look at the presets.ini file and try out some modifications. You can add fonts and tracks to the SD card and update your saber to use those fonts without reflashing, or re-order/increase/decrease your presets list without ever needing to open Arduino.

If for some reason you mess up the file, the saber will read from the backup .tmp file and boot up normally.

Of course, if you prefer to use a UI to do all of these changes, you can use the [WebUSB](../webusb.md) interface.
