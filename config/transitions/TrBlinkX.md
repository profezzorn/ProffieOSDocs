---
title: TrBlinkX
redirect_from:
  - /config/transitions/TrBlink.html
---

# Usage
```cpp
TrBlinkX<MILLIS_FUNCTION, N, WIDTH_FUNCTION>
TrBlink<MILLIS, N, WIDTH>
```

# Arguments
 * MILLIS_FUNCTION: FUNCTION
 * MILLIS: a number
 * N: a number
 * WIDTH_FUNCTION: FUNCTION, defaults to Int<16384>
 * WIDTH: a number, defaults to 16384
 * return value: TRANSITION

# Description
Blinks A-B N times in MILLIS, based on WIDTH (0 ~ 32768)
If WIDTH = 16384 A and B appear equally, lower decreases length of A, higher increases length of A

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/blink.h#L6
