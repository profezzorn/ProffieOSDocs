---
title: TrCenterWipeX
redirect_from:
  - /config/transitions/TrCenterWipe.html
---

# Usage
```cpp
TrCenterWipeX<POSITION_FUNCTION, MILLIS_FUNCTION>
TrCenterWipe<POSITION, MILLIS>
```

# Arguments
 * POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION
 * POSITION: Int
 * MILLIS: a number
 * return value: TRANSITION

# Description
In the beginning entire blade is color A, then color B
starts at the POSTION and extends up and down the blade
in the specified number of milliseconds.

# See Also
[TrCenterWipeInX](/config/transitions/TrCenterWipeInX.html), [TrWaveX](/config/transitions/TrWaveX.html), [TrSparkX](/config/transitions/TrSparkX.html), [Mult](/config/functions/Mult.html), [Percentage](/config/functions/Percentage.html), [Sum](/config/functions/Sum.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/center_wipe.h#L8
