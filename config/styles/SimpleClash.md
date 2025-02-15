---
title: SimpleClash
redirect_from:
  - /config/styles/SimpleClashL.html
---

# Usage
```cpp
SimpleClash&lt;BASE, CLASH_COLOR, CLASH_MILLIS&gt;
SimpleClashL&lt;CLASH_COLOR, CLASH_MILLIS&gt;
```

# Arguments
BASE: COLOR
CLASH_COLOR: COLOR (defaults to white)
CLASH_MILLIS: a number (defaults to 40)
return value: COLOR

# Description
Turns the blade to CLASH_COLOR for CLASH_MILLIS millseconds
when a clash occurs.

# See Also
[LocalizedClash](/config/styles/LocalizedClash.html), [SmoothStep](/config/functions/SmoothStep.html), [Layers](/config/styles/Layers.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/clash.h#L7
