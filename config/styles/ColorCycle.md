---
title: ColorCycle
---

# Usage
```cpp
ColorCycle&lt;COLOR, PERCENT, RPM&gt;
ColorCycle&lt;OFF_COLOR, OFF_PERCENT, OFF_RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, BASE_COLOR&gt;
```

# Arguments
OFF_COLOR, ON_COLOR, BASE_COLOR: COLOR
OFF_RPM, OFF_PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number
return value: COLOR

# Description
This is intended for a small ring of neopixels
A section of the ring is lit at the specified color
and rotates at the specified speed. The size of the
lit up section is defined by "percentage".
The arguments for this style are divided into two groups of
{ COLOR, PERCENT, RPM }, one for while the blade is OFF, and the other
while it's ON.
BASE_COLOR is the color of pixels not part of the lit section, so if PERCENT
is 0, the entire blade will be BASE_COLOR, and if PERCENT is 100, the entire blade
will be OFF_COLOR or ON_COLOR (depending on blade state).
FADE_TIME_MILLIS is the time taken to transition between the OFF and ON groups
of values.

# See Also
[Rgb](/config/styles/Rgb.html), [Rgb16](/config/styles/Rgb16.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/color_cycle.h#L7
