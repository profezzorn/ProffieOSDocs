---
title: SubBlade
---
SubBlade is used to split a string of pixels into multiple blades which can have their own styles. It takes three arguments:

```cpp
SubBlade(first_led, last_led, blade_definition)
```

Note the use of () instead of <>, as SubBlade is a regular function, not a template. If blade_definition is NULL, SubBlade() will use the blade definition from the previous call to SubBlade(). Since you can't have two blade definitions for the same string, you must use NULL to make multiple SubBlades refer to the same string of pixels.

Let's say we have a string that has one accent LED, one 8-pixel battery indicator and then a 100-LED blade. The blades[] array could then look something like this:

```cpp
SubBlade(9, 108, WS281XBlade<109, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>()),
SubBlade(1, 8, NULL),
SubBlade(0, 0, NULL),

```

Note that the first LED in the string is counted as zero, so there's always a -1 offset to your numbers to the actual pixels as you'd count them.
Also, The code doesn't really know what the "main blade" is.
They do not need to be in sequential order either.
The first style simply matches up with the first blade in the blades[] array,
second style matches the second blade in the blades[] array, etc.


Some more clarification and example:<br/>The data travels in series, one direction starting from the board, usually through accents and crystal chambers, and lastly the main blade.
This is why it's important to wire your LED strips following the arrows' direction.<br/>
For a blade with 130 pixels, the _first_led_ is 0, the _last_led_ is 129.<br/>
For a "blade" with 5 pixels (such as a NPXL hilt PCB connector), the _first_led_ is 0, the _last_led_ is 4.<br/>

Below we have a total of 135 pixels.<br/>
The first SubBlade is for the main blade which has 134 pixels.  It starts at 1 and ends at 134.<br/>
The second SubBlade is for the accent led / crystal chamber which has 1 pixel.  It starts and ends at 0.<br/>

They both use bladePin (data pad 1) and run in series. Power (-) for all pixels in series uses bladePowerPin2 and bladePowerPin3 (LED2 and LED3 pads, usually bridged).

```cpp
BladeConfig blades[] = {
  { 0,
    SubBlade(1, 134, WS281XBladePtr<135, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>()),	
    SubBlade(0, 0, NULL),
    CONFIGARRAY(presets),
  }
};
````

See also: [SubBladeZZ](/config/blades/subbladezz.html), [SubBladeReverse](/config/blades/subbladereverse.html), [SubBladeWithStride](/config/blades/subbladewithstride.html), [SubBladeWithList](/config/blades/subbladewithlist.html)
