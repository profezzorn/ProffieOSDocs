---
title: SubBladeWithStride
---
SubBladeWithStride lets you interleave multiple SubBlades.
Basically, it lets you make a blade out of every other pixel along the blade (or whatever interval you set).
It's mostly intended for using with the KR "Pixel Stick" blades which have 264 pixels wired in series, alternating between the top and bottom side.
By using SubBladeWithStride, you can make each side behave as it's own blade.
This alleviates the issue of animations rendering slower than intended due to the extra distance the blade presents within the same overall length.
Blade styles that have something like fire or stripes that move along the blade will appear slow travelling along 264 pixels.
So instead of editing every single argument that pertains to speed throughout the presets, we can make the blade appear as standard back-to-back 132 pixel strips by using SubBladeWithStride, and use blade styles as they are written for standard blades.

## SubBladeWithStride usage

Same as SubBlade, but with an additional argument of stride length is added like this:

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

See also: [SubBlade](/config/blades/subblade.html), [SubBladeReverse](/config/blades/subladereverse.html), [SubBladeZZ](/config/blades/subbbladezz.html), [SubBladeWithList](/config/blades/subbladewithlist.html)
