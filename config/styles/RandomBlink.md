---
title: RandomBlink
redirect_from:
  - /config/styles/RandomBlinkX.html
  - /config/styles/RandomBlinkL.html
---

# Usage
```cpp
RandomBlink&lt;MILLIHZ, COLOR1, COLOR2&gt;
RandomBlinkX&lt;MILLIHZ_CLASS, COLOR1, COLOR2&gt;
RandomBlinkL&lt;MILLIHZ_CLASS, COLOR1&gt;
```

# Arguments
MILLIHZ: integer
MILLHZ_CLASS: NUMBER
COLOR1: COLOR (defaults to WHITE)
COLOR2: COLOR (defaults to BLACK)
return value: COLOR

# Description
Each LED is randomly chosen as COLOR1 or COLOR2, then stays
that color for 1000/MILLIHZ seconds.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/random_blink.h#L4
