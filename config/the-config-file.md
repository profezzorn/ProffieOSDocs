---
title: The Config File
---
While EVERYTHING in ProffieOS is possible to change, most of the time, only the config file needs to be changed. The config file is really just some C++ code that specifies how the rest of the code should behave, but since many ProffieOS users are not C++ experts, this page describes the ProffieOS config files in more detail.

First, let's take a look at a typical config file:

```cpp
#ifdef CONFIG_TOP
#include "proffieboard_v1_config.h"
#define NUM_BLADES 1
#define NUM_BUTTONS 2
#define VOLUME 1000
const unsigned int maxLedsPerStrip = 144;
#define CLASH_THRESHOLD_G 1.0
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD
#endif

#ifdef CONFIG_PRESETS
Preset presets[] = {
   { "TeensySF", "tracks/venus.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(), "cyan"},
   { "SmthJedi", "tracks/mars.wav",
    StylePtr<InOutSparkTip<EASYBLADE(BLUE, WHITE), 300, 800> >(), "blue"},
   { "TthCrstl", "tracks/mars.wav",
    StylePtr<InOutHelper<EASYBLADE(OnSpark<GREEN>, WHITE), 300, 800> >(), "green"},
   { "TthCrstl", "tracks/uranus.wav",
    StyleStrobePtr<WHITE, Rainbow, 15, 300, 800>(), "strobe"},
   { "TeensySF", "tracks/venus.wav",
    &style_pov, "POV"},
   { "SmthJedi", "tracks/mars.wav",
    &style_charging, "Battery\nLevel"}
};
BladeConfig blades[] = {
 { 0, WS2811BladePtr<144, WS2811_ACTUALLY_800kHz | WS2811_GRB>(), CONFIGARRAY(presets) },
};
#endif

#ifdef CONFIG_BUTTONS
Button PowerButton(BUTTON_POWER, powerButtonPin, "pow");
Button AuxButton(BUTTON_AUX, auxPin, "aux");
#endif
```

As you can see, this file has three sections: TOP, PRESETS and BUTTONS.
Each section looks something like this:

```cpp
#ifdef CONFIG_NAME
Some stuff goes here
#endif
```

Where "NAME" is the name of the section.
While this file has three sections, some have four, and more may be possible in the future.
While each section can technically contain any valid C++ code, it is recommended to use the
sections as intended. Each section is explained in it's own page, to find out more, follow the links below:
* [The CONFIG_TOP section](/config/the-config_top-section.html)
* [The CONFIG_PRESETS section](/config/the-config_presets-section.html)
* [The CONFIG_BUTTONS section](/config/the-config_buttons-section.html)
* [The CONFIG_PROP section](/config/the-config_prop-section.html)
