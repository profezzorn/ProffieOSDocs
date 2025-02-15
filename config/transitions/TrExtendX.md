---
title: TrExtendX
redirect_from:
  - /config/transitions/TrExtend.html
---

# Usage
```cpp
TrExtendX<MILLIS_FUNCTION, TRANSITION>
TrExtend<MILLIS, TRANSITION>
```

# Arguments
 * MILLIS_FUNCTION: FUNCTION
 * TRANSITION: TRANSITION
 * MILLIS: a number
 * return value: TRANSITION

# Description
Runs the specified transition, then holds the
last value for some additional time specified by
MILLIS_FUNCTION.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/extend.h#L6
