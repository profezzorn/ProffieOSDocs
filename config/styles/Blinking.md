---
title: Blinking
redirect_from:
  - /config/styles/BlinkingX.html
  - /config/styles/BlinkingL.html
---

# Usage
```cpp
Blinking&lt;A, B, BLINK_MILLIS, BLINK_PROMILLE&gt;
BlinkingX&lt;A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC&gt;
BlinkingL&lt;B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC&gt;
```

# Arguments
A, B: COLOR
BLINK_MILLIS: a number
BLINK_PROMILLE: a number, defaults to 500
BLINK_MILLIS_FUNC: FUNCTION
BLINK_PROMILLE_FUNC: FUNCTION
return value: COLOR

# Description
Switches between A and B.
A full cycle from A to B and back again takes BLINK_MILLIS milliseconds.
If BLINK_PROMILLE is 500, we select A for the first half and B for the
second half. If BLINK_PROMILLE is smaller, we get less A and more B.
If BLINK_PROMILLE is 0, we get all B.
If BLINK_PROMILLE is 1000 we get all A.


# See Also
[Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/blinking.h#L6
