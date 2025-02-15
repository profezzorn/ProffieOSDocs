---
title: CircularSectionF
---

# Usage
```cpp
CircularSectionF<POSITION, FRACTION>
```

# Arguments
POSITION: FUNCTION position on the circle or blade, 0-32768
FRACTION: FUNCTION how much of the blade to light up, 0 = none, 32768 = all of it
return value: FUNCTION

# Description
Returns 32768 for LEDs near the position with wrap-around.
Could be used with MarbleF<> for a marble effect, or with
Saw<> for a spinning/colorcycle type effect.
Example: If POSITION = 0 and FRACTION = 16384, then this function
will return 32768 for the first 25% and the last 25% of the blade
and 0 for the rest of the LEDs.

# See Also
[MarbleF](/config/functions/MarbleF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/circular_section.h#L6
