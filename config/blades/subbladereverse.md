---
title: SubBladeReverse
---
SubBladeReverse is works exactly like [SubBlade](/config/blades/subblade.html), except, that the pixels in the indexed range are addressed in reverse order. This can be useful to create zig-zag blades, where the data travels up one strip, than DOWN the other one. Such a blade lets you address all the pixels individually without needing more data lines.

Example, if you have a 100-pixel zig-zag blade:

```cpp
SubBlade(0, 99, WS281XBladePtr<200, bladePtr, Color8::GRB>()),
SubBladeReverse(100, 199, NULL)
```

Note that you'll need to increase maxLedsPerString to 200.
Also, the first LED in the string is counted as zero, so there's always a -1 offset to your numbers to the actual pixels as you'd count them.

See also: [SubBlade](/config/blades/subblade.html), [SubBladeWithStride](/config/blades/subladewithstride.html), [SubBladeZZ](/config/blades/subbbladezz.html), [SubBladeWithList](/config/blades/subbladewithlist.html)
