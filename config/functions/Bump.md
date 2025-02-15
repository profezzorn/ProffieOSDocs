---
title: Bump
---

# Usage
```cpp
Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>
```

# Arguments
BUMP_POSITION, BUMP_WIDTH_FRACTION: INTEGER

# Description
Returns different values for each LED, forming a bump shape.
If BUMP_POSITION is 0, bump will be at the hilt.
If BUMP_POSITION is 32768, the bump will be at the tip.
If BUMP_WIDTH_FRACTION is 1, bump will be extremely narrow.
If BUMP_WIDTH_FRACTION is 32768, it will fill up most/all of the blade.

# See Also
[HumpFlickerFX](/config/functions/HumpFlickerFX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/bump.h#L4
