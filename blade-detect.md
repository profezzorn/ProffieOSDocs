---
title: Blade Detect
---
Blade Detect typically uses a floating pin on the hilt side PCB that only gets connected when the ring of the blade side PCB contacts it and another pin in the same ring footprint. A latching button or switch could also be used.  
This latching action is detected by the board and triggers a sound and a swap of which blade configuration is used; NO_BLADE or a blade present one. The active blades[] array specifies which CONFIGARRAY (bank of presets) to use, so you get to have a different group of presets used depending on the presence of a blade or not.  
Example BladesConfig using Blade Detect:
```
    BladesConfig blades[] = {
      { 0,
        WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
        CONFIGARRAY(blade_in) },

      { NO_BLADE,
        WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
        CONFIGARRAY(no_blade), "nbsave" }
    };
```

Please note the "nbsave" part, which will make ProffieOS save presets.ini and other related save files into the "nbsave/" directory on the SD card. If that directory doesn't exist, saving will fail, but that might be ok for the no-blade case.

  
Blade detection is activated by using the BLADE_DETECT_PIN define in the [CONFIG_TOP](config/the-config_top-section) section of the config file.  
The pin number can either be just a number, or a symbolic name like "blade2Pin". See these 2 examples:   

    #define BLADE_DETECT_PIN 0
or  

    #define BLADE_DETECT_PIN blade4Pin  

The blade detect pin will be monitored continuously, when it changes, the Blade ID routines will be re-triggered. In addition, when not connected to anything, Blade ID will be offset by the value of NO_BLADE, which equals a billion.

The detection works by repeatedly switching between pull-up and pull-down mode and see if the input follows, or if it stays put at high or low. That means that it doesn't matter if the blade ID pin is connected to GND or BATT+, which is a good thing, because when connected to the '-' pad on a neopixel strip, that can flip between high and low when the FETs are turned on/off.

Please note that Blade Detect is separate from Blade ID and cannot use the same pin.  
See more about [Blade ID here](blade-id.md).
