---
title: TrBoingX
redirect_from:
  - /config/transitions/TrBoing.html
---

# Usage
```cpp
TrBoingX<MILLIS_FUNCTION, N>
TrBoing<MILLIS, N>
```

# Arguments
 * MILLIS_FUNCTION: FUNCTION
 * MILLIS: a number
 * N: a number
 * return value: TRANSITION

# Description
Similar to TrFade, but transitions back and forth between the two
colors several times. (As specified by N). If N is 0, it's equal to
TrFade. If N is 1 it transitions A-B-A-B, if N is 2, it is A-B-A-B-A-B,
and so on.

# See Also
[TrFadeX](/config/transitions/TrFadeX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/boing.h#L6
