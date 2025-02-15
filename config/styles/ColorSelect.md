---
title: ColorSelect
---

# Usage
```cpp
ColorSelect<SELECTION, TRANSITION, COLOR1, COLOR2, ...>
```

# Arguments
 * SELECTION: function
 * TRANSITION: transition
 * COLOR1, COLOR2, ...:  COLOR
 * Return value: COLOR

# Description
Decides what color to return based on the current selection.
The returned color will be selection % N (where N is the number of colors arguments).
When the selection changes, the transition will be used to change from the old color to the new color.

# See Also
[Variation](/config/functions/Variation.html), [Mix](/config/styles/Mix.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/color_select.h#L8
