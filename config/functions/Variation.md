---
title: Variation
---

# Usage
```cpp
Variation
```

# Arguments
No arguments

# Description
Returns 0-32768 based on current variation.
returned value: FUNCTION
Note that using Variation in your style means that the
the automatic color rotation is turned off. The color wheel
menu is unaffected, but the style is now responsible for actually
changing the color.
Note that if any blade styles are using ColorChange<>,
the variation will return "ticked" values: 0, 1, 2, etc.

# See Also
[ColorChange](/config/styles/ColorChange.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/variation.h#L6
