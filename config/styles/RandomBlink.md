---
title: RandomBlink
redirect_from:
  - /config/styles/RandomBlinkX.html
  - /config/styles/RandomBlinkL.html
---

# Usage
```cpp
RandomBlink<MILLIHZ, COLOR1, COLOR2>
RandomBlinkX<MILLIHZ_CLASS, COLOR1, COLOR2>
RandomBlinkL<MILLIHZ_CLASS, COLOR1>
```

# Arguments
 * MILLIHZ: integer
 * MILLHZ_CLASS: NUMBER
 * COLOR1: COLOR (defaults to WHITE)
 * COLOR2: COLOR (defaults to BLACK)
 * return value: COLOR

# Description
Each LED is randomly chosen as COLOR1 or COLOR2, then stays
that color for 1000/MILLIHZ seconds.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/random_blink.h#L4
