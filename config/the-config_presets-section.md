---
title: The CONFIG_PRESETS section
---
The main purpose of the CONFIG_PRESETS section, is to define the blades[] array. However, the blades[] array contains pointers to the presets[] array(s), so we must also define those in this section. It is also possible to put custom LED structs, style aliases and other such things in this section.

First, let's explain what an array is: It is a repeated list of data. The general format of an array is something like:

    TYPE NAME[] = { first_entry, second_entry, third_entry };

The TYPE specifies what kind of data goes in each entry. For the blades[] array, the type is BladeConfig, and for the presets[] array, the type is Preset.

A BladeConfig looks something like this:

    {
      0,  // Blade ID resistance
      blade definitions,   // NUM_BLADES specifies how many blade definitions there are
      CONFIGARRAY(presets),
    }

If there are multiple BladeConfigs, ProffieOS will measure the resistance between the **blade data pin and GND** and use the BladeConfig that has the closest [Blade ID](../blade-id.html). This decides what blade definitions and preset arrays to use.<br/>
Also, if you use #define SAVE_STATE in your config, you can save states in a subfolder on your SD card for each blade array by adding a quoted save name to the end of the BladeConfig [] array, similar to the quoted "name" at the end of a preset.  For example:

    BladeConfig blades[] = {
    { 0, WS281XBladePtr<0, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(NBpresets), 
    "No_Blade_save", },
    { 33000, WS281XBladePtr<123, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), 
    CONFIGARRAY(34presets), "My34inch_blade_save", },
    };

will create 2 folders on the SD card named No_Blade_save and My34inch_blade_save, each containing the last used preset, color change state, and last used volume with each blade.

Each blade definition should use one of the following: (click for more info)

* [WS281XBladePtr](blades/ws281xbladeptr.html) - new style pixel blade definition
* [WS2811BladePtr](blades/ws2811bladeptr.html) - old style pixel blade definition
* [SimpleBladePtr](blades/simplebladeptr.html) - blade for single LEDs and LED stars
* [StringBladePtr](blades/stringbladeptr.html) - blade for old-fashioned 6-segment blades (or more with external FETs)
* [SubBlade](blades/subblade.html) - A blade from a sub-section of a pixel string
* [SubBladeReverse](blades/subbladereverse.html) - Like SubBlade, but reverses indexing for zig-zag blades
* [FASTLEDBladePtr](blades/fastledbladeptr.html) - EXPERIMENTAL, used for dotstar blades
* [DimBlade](blades/dimblade.html) - Similar to SubBlade, but reduces the brightness of the blade.
* [SpiBladePtr](blades/spibladeptr.html) - Non-experimental, but somewhat slow dotstar support.

The Preset array is made up of Presets, see [Preset Configuration](preset-configuration.html) for details.

Note that that there can be multiple preset arrays, and the name of the preset array is not important, as long as the blade array uses the right name. Example:

    Preset p1[] = {
      {"font1", "track1.wav", StyleNormalPtr<BLUE, WHITE, 800, 300>(), "blue preset"}
    };
    Preset p2[] = {
      {"font2", "track2.wav", StyleNormalPtr<RED, WHITE, 800, 300>(), "red preset"}
    };   

    BladesConfig blades[] = {
      { 5000,
        WS2811BladePtr<144, WS2811_ACTUALLY_800kHz | WS2811_GRB>(),
        CONFIGARRAY(p1)
      },
      { 10000,
        WS2811BladePtr<144, WS2811_ACTUALLY_800kHz | WS2811_GRB>(),
        CONFIGARRAY(p2)
      }
    };

In this example, the Blade ID is used to select between the red and blue presets.  Also note that spaces and newlines are basically ignored, so we are free to write the configuration on one line or many lines as we please.

If you have RFID_SERIAL in [the CONFIG_TOP section](the-config_top-section.html), then you will also need to have a RFID_Commands array, which could look like this:

    RFID_Command RFID_Commands[] = {
      { 0x0000000C04ULL,    "change_preset", "0" },
      { 0x09003A8CDCULL,    "change_preset", "1" },
    };

This will change preset to 0 when the RFID reader sees card with ID C04 (which happens to be a green crystal) and change to preset 1 when it sees something with a card ID of 3a8cdc. Any serial monitor command can be used.


