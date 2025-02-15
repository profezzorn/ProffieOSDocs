---
title: ColorChange
---

# Usage
```cpp
ColorChange<TRANSITION, COLOR1, COLOR2, ...>
```

# Arguments
TRANSITION: transition
COLOR1, COLOR2, ...:  COLOR
Return value: COLOR

# Description
Decides what color to return based on the current variation.
The returned color will be current_variation % N (where N is the number of colors arguments).
When the variation changes, the transition will be used to change from the old color to the new color.

# See Also
[Variation](/config/functions/Variation.html), [ColorSelect](/config/styles/ColorSelect.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/colorchange.h#L7
