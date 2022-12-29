---
title: WS2811BladePtr
---
WS2811BladePtr is an older version of [WS281XBladePtr](/config/blades/ws281xbladeptr.html). I recommend using WS281XBladePtr instead this documentation can be helpful to understand older config files though.

WS2811BladePtr takes 7 arguments, but only two are actually required.

     WS2811BladePtr<leds, config, data_pin, power_pins, pin_class, reset_us, t1h, t0h>

All the arguments except for "config" behave the same as in [WS281XBladePtr](/config/blades/ws281xbladeptr.html).

The config specifies both the byte order and the frequency. The byte order is one of:

    WS2811_RGB
    WS2811_RBG
    WS2811_GRB
    WS2811_GBR

If no byte order, it defaults to RGB, which is probably not what you want.
The frequency is one of:

    WS2811_800kHz
    WS2811_400kHz
    WS2813_800kHz
    WS2811_580kHz
    WS2811_ACTUALLY_800kHz

Note that the 800kHz ones actually use 740kHz. And the WS2811 and WS2813 ones are identical since all of them use a timeout of 300us.

The frequency and byte order are combined by using the | operator, like this:

    WS2811_800kHz | WS2811_GRB
