---
title: Blade Detect
redirect_from:
  - /blade-detect.html
---
Blade Detect typically uses a floating pin on the hilt side PCB that only gets connected when the ring of the blade side PCB contacts it and another pin in the same ring footprint. A latching button or switch could also be used.  
This latching action is detected by the board and triggers a sound and a swap of which blade configuration is used; NO_BLADE or a blade present one. The active blades[] array specifies which CONFIGARRAY (bank of presets) to use, so you get to have a different group of presets used depending on the presence of a blade or not.  
Example BladesConfig using Blade Detect:
```cpp
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

  
Blade detection is activated by using the BLADE_DETECT_PIN define in the [CONFIG_TOP](/config/the-config_top-section) section of the config file.  
The pin number can either be just a number, or a symbolic name like "blade2Pin". See these 2 examples:   

```cpp
#define BLADE_DETECT_PIN 0
```
or  
```cpp
#define BLADE_DETECT_PIN blade4Pin  
```

The blade detect pin will be monitored continuously, when it changes, the Blade ID routines will be re-triggered. In addition, when not connected to anything, Blade ID will be offset by the value of NO_BLADE, which equals a billion.

The detection works by repeatedly switching between pull-up and pull-down mode and see if the input follows, or if it stays put at high or low. That means that it doesn't matter if the blade ID pin is connected to GND or BATT+, which is a good thing, because when connected to the '-' pad on an LED pixel strip, that can flip between high and low when the FETs are turned on/off.

Here's an example template of a config file formatted to use Blade Detect:  
```cpp
// This is a simplified config file template set up for Blade Detect.

#ifdef CONFIG_TOP
#define BLADE_DETECT_PIN blade4Pin
// other defines go here
#endif

#ifdef CONFIG_PROP
#include "../props/PROP_FILE_OF_CHOICE_GOES_HERE.h"
#endif


#ifdef CONFIG_PRESETS

Preset no_blade[] = {

{ "font", "tracks/track",
  StylePtr<Blue>(), "preset name"},

};

//---------------------------------------------------------------

Preset blade_in[] = {

{ "font", "tracks/track",
  StylePtr<Red>(), "preset name"},

};



BladesConfig blades[] = {
  { NO_BLADE,
    WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
    CONFIGARRAY(no_blade), "no_blade_Save" },
  { 0,
    WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
    CONFIGARRAY(blade_in), "blade_in_Save" }

};
#endif

#ifdef CONFIG_BUTTONS
Button PowerButton(BUTTON_POWER, powerButtonPin, "pow"); 
Button AuxButton(BUTTON_AUX, auxPin, "aux");
#endif

```  

Please note that Blade Detect is separate from Blade ID and cannot use the same pin.  
See more about [Blade ID here](blade-id.html).
