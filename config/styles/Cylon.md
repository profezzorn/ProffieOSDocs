---
title: Cylon
---

# Usage
```cpp
Cylon<COLOR, PERCENT, RPM>
Cylon<OFF_COLOR, OFF_PERCENT, OFF_RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, BASE_COLOR>
```

# Arguments
OFF_COLOR, ON_COLOR, BASE_COLOR: COLOR
OFF_RPM, OFF_PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number
return value: COLOR

# Description
Cylon/Knight Rider effect, a section of the strip is
lit up and moves back and forth. Speed, color and fraction
illuminated can be configured separately for on and off
states.
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
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/cylon.h#L7
