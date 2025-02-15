---
title: Pulsing
redirect_from:
  - /config/styles/PulsingX.html
  - /config/styles/PulsingL.html
---

# Usage
```cpp
Pulsing<A, B, PULSE_MILLIS>
PulsingX<A, B, PULSE_MILLIS_FUNC>
PulsingL<B, PULSE_MILLIS_FUNC>
```

# Arguments
 * A, B: COLOR
 * PULSE_MILLIS: a number
 * PULSE_MILLIS_FUNC: FUNCTION
 * return value: COLOR

# Description
Goes back and forth between COLOR1 and COLOR2.
A full transition from COLOR1 to COLOR2 and back again takes PULSE_MILLIS milliseconds.

# See Also
[Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/pulsing.h#L6
