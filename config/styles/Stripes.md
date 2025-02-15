---
title: Stripes
redirect_from:
  - /config/styles/StripesX.html
---

# Usage
```cpp
Stripes&lt;WIDTH, SPEED, COLOR1, COLOR2, ... &gt;
StripesX&lt;WIDTH_CLASS, SPEED, COLOR1, COLOR2, ... &gt;
```

# Arguments
WIDTH: integer (start with 1000, then adjust up or down)
WIDTH_CLASS: INTEGER
SPEED: integer  (start with 1000, then adjust up or down)
COLOR1, COLOR2: COLOR
return value: COLOR

# Description
Works like Rainbow, but with any colors you like.
WIDTH determines width of stripes
SPEED determines movement speed

If you have a ring of LEDs and you want the stripes to line up,
you'll need to set WIDTH using the following formula:
WIDTH = 50000 * NUM_LEDS_IN_RING / (NUM_COLORS * REPETITIONS * 341)

# See Also
[HardStripes](/config/styles/HardStripes.html), [Rainbow](/config/styles/Rainbow.html), [Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/stripes.h#L7
