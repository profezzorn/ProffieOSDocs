---
title: TrCenterWipeInX
redirect_from:
  - /config/transitions/TrCenterWipeIn.html
---

# Usage
```cpp
TrCenterWipeInX<POSITION_FUNCTION, MILLIS_FUNCTION>
TrCenterWipeIn<POSITION, MILLIS>
```

# Arguments
POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION
POSITION: Int
MILLIS: a number
return value: TRANSITION

# Description
In the beginning entire blade is color A, then color B
starts at the ends and moves toward POSITION
in the specified number of milliseconds.

# See Also
[TrCenterWipeX](/config/transitions/TrCenterWipeX.html), [TrWaveX](/config/transitions/TrWaveX.html), [TrSparkX](/config/transitions/TrSparkX.html), [Mult](/config/functions/Mult.html), [Percentage](/config/functions/Percentage.html), [Sum](/config/functions/Sum.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/center_wipe.h#L46
