---
title: Strobe
redirect_from:
  - /config/styles/StrobeX.html
  - /config/styles/StrobeL.html
---

# Usage
```cpp
Strobe<BASE, STROBE_COLOR, STROBE_FREQUENCY, STROBE_MILLIS>
StrobeX<BASE, STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>
StrobeL<STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>
```

# Arguments
 * BASE, STROBE_COLOR: COLOR
 * STROBE_FREQUENCY, STROBE_MILLIS: a number
 * STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION
 * return value: COLOR

# Description
Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS
STROBE_FREQUENCY times per second.

# See Also
[Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/strobe.h#L6
