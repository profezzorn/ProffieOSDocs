---
title: SubBladeZZ
---

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

See also: [SubBlade](/config/blades/subblade.html), [SubBladeReverse](/config/blades/subladereverse.html), [SubBladeWithStride](/config/blades/subbbladewithstride.html), [SubBladeWithList](/config/blades/subbladewithlist.html)
