---
title: HardStripes
redirect_from:
  - /config/styles/HardStripesX.html
---

# Usage
```cpp
HardStripes<WIDTH, SPEED, COLOR1, COLOR2, ... >
HardStripesX<WIDTH_CLASS, SPEED, COLOR1, COLOR2, ... >
```

# Arguments
WIDTH: integer (start with 1000, then adjust up or down)
WIDTH_CLASS: INTEGER
SPEED: integer  (start with 1000, then adjust up or down)
COLOR1, COLOR2: COLOR
return value: COLOR

# Description
Works like Stripes, but with no gradient between color segments..
* Note * Regular Stripes is recommended for very slow speeds.
Without a 1 pixel gradient smoothing the changing pixel color,
the animation can seem a little "choppy". At faster speeds, this is not apparent.

# See Also
[Stripes](/config/styles/Stripes.html), [Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/stripes.h#L22
