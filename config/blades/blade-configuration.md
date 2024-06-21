---
title: Blade Configuration
---
Proffie OS allows the use of multiple blades configurations.

All blades are defined in object array of type _BladeConfig_.
Blade selection works with resistance measurement on the ID pin of the board. If no more then one blade configurations are defined in the array, it will be selected regardless of the resistance on the pin.

Example:
The following code defines two blade configurations. 
If you connect 2.6k Resistor between ID and GND pin, the saber board will be configured to use neopixel setup with style configuration in the _presets_ array. Similarly the second configuration switches to Tri-Cree setup.
To learn how to configure presets array check out the [Preset Configuration](/config/preset-configuration.html) page.
```cpp
BladeConfig blades[] = {
  {2600, WS2811BladePtr<144, WS2811_ACTUALLY_800kHz | WS2811_GRB>(), CONFIGARRAY(presets) },
  {13000, SimpleBladePtr<CreeXPL, CreeXPL, CreeXPL, NoLED>(), CONFIGARRAY(white_presets) },
};
```
For more information about the blades array, see [The CONFIG_PRESETS section](/config/the-config_presets-section.html) page.

## LED Support
Most major LEDs that are used in the saber practice are already defined as templates
(CreeXPE2White, CreeXPE2Blue and etc.), and their current and voltage values are defined so that the PWM engine can drive them accordingly.

**Note**: For direct drive it is still good practice to use a resistor to prolong the LED dye lifespan.

For more info on direct drive LEDs, see [this page](/config/blades/led-configuration.html).

## SubBlade
When using addressable LED strip, a single strip can be separated into a couple of sub blades with their own style configuration and behaviour. This is really useful when you want to use only one data pin for all the addressable LEDs in your setup.

Example for SubBlade usage:
```cpp
BladeConfig blades[] = {
{ 0,
   SubBlade(0, 1, WS2811BladePtr<146, WS2811_580kHz>()),
   SubBlade(2, 14, NULL),  //Quilon A
   SubBlade(15,26, NULL), //Quilon B
   SubBlade(27, 145, NULL) //Main Blade
   CONFIGARRAY(presets) 
}
};
```

Sample Preset that works with sub-blades:
```cpp
#define FIRE1_SPEED 2
#define FIRE1_DELAY 800
#define FIRE1_NORMAL 0, 1000, 2
#define FIRE1_CLASH  3000, 0, 0
#define FIRE1_LOCKUP 0, 5000, 10
#define FIRE1PTR(NUM, DELAY) \
  StyleFirePtr<RED, YELLOW, NUM, DELAY, FIRE1_SPEED, \
    FIRE1_NORMAL, FIRE1_CLASH, FIRE1_LOCKUP>()


 Preset presets[] = {
{ "font01", "tracks/title.wav",
   StyleNormalPtr<AudioFlicker<YELLOW, WHITE>, RED, 300, 800>, //Accent Pixel Style
   FIRE1PTR(1, FIRE1_DELAY),  //Quilon A Style
   FIRE1PTR(2, FIRE1_DELAY),  //Quilon A Style
   FIRE1PTR(0, 0), //Main Blade Style
 }
};
```
For more details check out the [SubBlade](/config/blades/subblade.html) page.

