---
title: TwistAngle
---

# Usage
```cpp
TwistAngle<N, OFFSET>
```

# Arguments
 * OFFSET: Adjustable offset (0-32768) to make the twistangle values line up with how you hold the hilt.
 * N : Number of times the values goes from 0 to 32768 and back per hilt revolution.
 * returned value: FUNCTION, same for all leds

# Description
Returns 0-32768 based on angle of twist

# See Also
[TwistAcceleration](/config/functions/TwistAcceleration.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/twist_angle.h#L6
