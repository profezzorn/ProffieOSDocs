---
title: LocalizedClash
redirect_from:
  - /config/styles/LocalizedClashL.html
---

# Usage
```cpp
LocalizedClash<BASE, CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>
LocalizedClashL<CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>
```

# Arguments
 * BASE: COLOR
 * CLASH_COLOR: COLOR (defaults to white)
 * CLASH_MILLIS: a number (defaults to 40)
 * return value: COLOR

# Description
Similar to SimpleClash, but lights up a portion of the blade.
The fraction of the blade is defined by CLASH_WIDTH_PERCENT
The location of the clash is random within the middle half of the blade.
Localized clashes should work well with stabs with no modifications.

# See Also
[SimpleClash](/config/styles/SimpleClash.html), [SmoothStep](/config/functions/SmoothStep.html), [Layers](/config/styles/Layers.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/clash.h#L58
