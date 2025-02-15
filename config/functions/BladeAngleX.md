---
title: BladeAngleX
---

# Usage
```cpp
BladeAngleX<MIN, MAX>
```

# Arguments
MIN : FUNCTION (defaults to Int<0>)
MAX : FUNCTION (defaults to Int<32768>)
Returns: 0-32768 based on angle of blade

# Description
MIN and MAX specifies the range of angles which are used.
For MIN and MAX 0 means down and 32768 means up and 16384 means
pointing towards the horizon.
So if MIN=16484 and MAX=32768, BladeAngle will return zero when you
point the blade towards the horizon and 32768 when you point it
straight up. Any angle below the horizon will also return zero.
returned value: FUNCTION, same for all LEDs.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/blade_angle.h#L6
