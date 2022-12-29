---
title: Glossary
---

## [Arduino](https://www.arduino.cc/en/software)
A cross-platform program that attempts to make software development for embedded platforms simple.

## [config file](/config/the-config-file.md)
A file that specifies everything ProffieOS needs to know to make your saber (or other prop) work.

## #define
In ProffieOS, we use C++ defines to specify which features to turn on and off. See [the CONFIG_TOP section](/config/the-config_top-section.md) for a list of available defines. Note that there may be more defines available depending on what prop file you use.

## [Blade Detect](/blade-detect.md)
Let's ProffieOS detect when a blade is attached/detached.

## [Blade ID](/blade-id.md)
Let's ProffieOS detect which blade is attached.

## FET
Field Effect Transistor. Basically a switch that can be controlled electically. A Proffieboard v2.2 has 6 of these that are used to enable/disable power to LEDs and other things.

## Kill key
A small plug that plugs into a charge port on a saber, but which does not do any charging. Instead, it just causes the battery to be disconnected. A kill key is an alternative to having an on/off switch to disconnect the battery when you're not using your saber.

## Neopixels
The Adafruit brand name for LEDs that can be controlled using the WS2811 protocol.

## OLED
Abbreviation meaning "Organic Light Emitting Diode", but in this context, we use it to mean a small display connected to the Proffieboard which can show messages and images.

## [Preset](/config/the_config_presets_section.md)
A combination of a font, a track and one or more styles. "factory settings" are configured in the config file, but changes can be made with edit mode or the ProffieOS workbench. Such changes are stored in prests.ini on the SD card.

## Port
Short for "serial port". Used in Arduino to communicate with your Proffieboard. Make sure to select the right one under Arduino -> Tools -> Port.

## Profezzorn
Fredrik Hubinette's online alias. You know, the guy who designed the Proffieboards, wrote ProffieOS and various other stuff. If you want to get in touch with Profezzorn, see the [How to Contact Profezzorn Page](/contacting-profezzorn.md).

## Prop file
A file that controls most of the behaviors of ProffieOS. In particular, it controls which button does what.
Several prop files come with ProffieOS, and you can also make your own. See [the CONFIG_PROP section](/config/the-config_prop-section.md) to learn how to specify which prop file to use in your config file.

## presets.ini
A file that stores changes made to your presets.

## [Serial Monitor](/tools/serial-monitor.md)
A window in Arduino which lets you type commands and receive text-based output from a Proffieboard. (Or any other Arduino-compatible board.)

## Smoothswing
An algorithm for how to make Star Wars-style lightsaber sounds from motion events.

## TeensySaber
This is what ProffieOS used to be called. It is also the name of the teensy-based boards that were used with ProffieOS before Proffieboards.

## [WebUsb](/webusb.md)
A way to connect a browser to a Proffieboard. Lets you use the ProffieOS workbench.

## [Zadig](/tools/zadig.md)
A windows program that allows you to specify which driver to use for a USB device.

