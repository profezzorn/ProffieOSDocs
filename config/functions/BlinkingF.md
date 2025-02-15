---
title: BlinkingF
---

# Usage
```cpp
BlinkingF&lt;A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC&gt;
```

# Arguments
BLINK_MILLIS: a number
BLINK_PROMILLE: a number, defaults to 500
BLINK_MILLIS_FUNC: FUNCTION
BLINK_PROMILLE_FUNC: FUNCTION
return value: FUNCTION

# Description
Switches between 0 and 32768
A full cycle from 0 to 328768 and back again takes BLINK_MILLIS milliseconds.
If BLINK_PROMILLE is 500, we select A for the first half and B for the
second half. If BLINK_PROMILLE is smaller, we get less A and more B.
If BLINK_PROMILLE is 0, we get all 0.
If BLINK_PROMILLE is 1000 we get all 32768.


# See Also
[Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/blinking.h#L6
