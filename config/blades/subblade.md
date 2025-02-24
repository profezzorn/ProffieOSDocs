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

## SubBladeWithStride

SubBladeWithStride lets you interleave multiple SubBlades.
Basically, it lets you make a blade out of every other pixel along the blade (or whatever interval you set).
It's mostly intended for using with the KR "Pixel Stick" blades which have 264 pixels wired in series, alternating between the top and bottom side.
By using SubBladeWithStride, you can make each side behave as it's own blade.
This alleviates the issue of animations rendering slower than intended due to the extra distance the blade presents within the same overall length.
Blade styles that have something like fire or stripes that move along the blade will appear slow travelling along 264 pixels.
So instead of editing every single argument that pertains to speed throughout the presets, we can make the blade appear as standard back-to-back 132 pixel strips by using SubBladeWithStride, and use blade styles as they are written for standard blades.

## SubBladeWithStride usage

Same as above, but an additional argument of stride length is added like this:

```cpp
SubBladeWithStride(first_led, last_led, stride_length, blade_definition)
```

So to split the 264 pixel strip into 2 x 132 pixel blades, we would do this :

```cpp
BladeConfig blades[] = {
  { 0,
    SubBladeWithStride (0, 262, 2, WS281XBladePtr<264, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >() ),
    SubBladeWithStride (1, 263, 2, NULL),
    CONFIGARRAY(presets),
  }
};
```

## SubBladeZZ

SubBladeZZ is similar to SubBladeWithStride, but each row changes direction. This is useful when pixels are arranged in some sort of grid, and the data signal goes up, down, up, down or left, right, left, right. SubBladeZZ was added in ProffieOS 7.x.

The usage is similar to SubBladeWithStride, but adds a "column" parameter, because you can't just adjust "first_led" to select which column you want.
```cpp
SubBladeZZ(first_led, last_led, stride, column, blade_definition)
```

So, if we have a grid of 3x5 leds, where data is going left, then right, alternatenating for each column. Our blade definition might look something like:
```
BladeConfig blades[] = {
  { 0,
    SubBladeZZ(0, 14, 3, 0, WS281XBladePtr<15, bladePin, Color8::GRB, PowerPINS<bladePowerPin6> >() ),
    SubBladeZZ(0, 14, 3, 1, NULL),
    SubBladeZZ(0, 14, 3, 2, NULL)
    CONFIGARRAY(presets),
  }
};
```

Now we have one blade for each column in the grid.


