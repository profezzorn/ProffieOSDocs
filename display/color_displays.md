---
title: Color Displays
---

# Supported Displays

ProffieOS currently has support for four types of color displays:
1. [DFRobot 847 160x80 0.96"](https://wiki.dfrobot.com/0.96_Inch_160_80_Color_SPI_TFT_Display_SKU_DFR0847) - small display suitable for sabers
2. [Adafruit 358 128x128 1.8"](https://www.adafruit.com/product/358) - You can find similar displays on ebay, which should also work.
3. [Adafruit 5206 280x240 1.69"](https://www.adafruit.com/product/5206) - higher resolution display
4. [Adafruit 4311 320x240 2.0"](https://www.adafruit.com/product/4311) - biggest, highest resolution

More will be added in the future.

I highly recommend using an [eyespi breakout board](https://www.adafruit.com/product/5613) to connect to the displays, but it is also possible to solder directly to the displays.

Note that you will need a V3 Proffieboard to use color displays.

# Wiring and Configuration
Please use the [Proffieboard configuration generator](https://fredrik.hubbe.net/lightsaber/v6/configurator.html) to find out how to wire up the display and to see what to put int the configuration file. For the rest of the examples below, we'll be using the DFRobot display for examples.

# SCR, PQF and Layers
Color displays in ProffieOS are implemented using layers, similar to how the Layer<> blade style works. However, the indidvidual layers do not come from other styles, but are instead read from PQF files on the SD card. PQF is a simple image/video compression format specifically created for this purpose. SCR files are fairly simple text files which specifies what each layer should be doing.

So, when a clash occurs, ProffieOS will find and read the approperiate SCR file, using the same EFFECT file system which is used to play sound effects and OLED images. Then it will read that file, and follow the instructions in it. Each layer can have a different set of instructions, separated by a line that just says "layer", example:

```ini
file=background.pqf
layer
file=clash.pqf
```

This file will play "background.pqf" on the first (bottom) layer, and "clash.pqf" on the second layer.
For a full description of how SCR files work, read the [SCR Page](/display/SCR.html).

# PQF files
PQF files files can contain images, animations, loops, and even complicated things like counters. This allows for a large set of complicated animations without having to write code for it, which would take up a lot of space on the Proffieboard. The [PQF page](/display/PQF.html) has descriptions of what PQF can do and how to convert images and animations to PQF.

# A note about speed
Driving color displays is a heavy operation for a Proffieboard. For the smallest displays, achiving a reasonably high frame rate is usually not a problem, but I highly recommen compiling with the "Fastest" setting to make the display work as well as it can. Note that "Fastest" uses a lot of memory, so the number of presets will be limited.

For larger displays, the maximum frame rate will depend on the complexity of the content. If PQF is able to compress the content well, then good frame rates are still possible, but complex content will may not be able to play at full speed.

Using layers also reduces the maximum possible frame rate. Fully transparent and fully opaque pixels are fairly quick to draw, but semi-transparent pixels are slower, so please use them sparingly. Some transparent pixels surrounding an otherwise opaque object should be fine, but drawing a "haze" or a bunch of glass effects is likely going to be too slow.

# Effects
The code that reads SCR files currently supports the following set of files:
* boot - played on boot (falls back on font)
* font - played when switching presets
* blst - played on blast
* clsh - played on clash
* force - played on force push
* preon - played on preon
* out - played on ignition
* in - played on retraction
* pstoff - played on post-off
* lock - played during lockup (repeats)
* pli - played when battery status is requested
* idle - played when off (repeats)
* on - played when on (repeats)
* lowbatt - played when battery is low

Normally, the SCR file should be in a sub-directory of the font, which is named by the resolution, so if your font directory is "smthjedi", and your screen is 168x80, then the clash SCR file should be called "smthjedi/180x80/clash.scr". Of course you can also have multiple "clash.scr" files, like "smthjedi/180x80/clash01.scr", "smthjedi/180x80/clash02.scr", etc.

A sample virtual crystal chamber, with a battery meter on a sparate layer can be found here:
https://github.com/profezzorn/ProffieColorImages/tree/main/examples/crystal_chamber_160x80



