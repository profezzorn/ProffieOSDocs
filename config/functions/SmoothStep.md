---
title: SmoothStep
---

# Usage
```cpp
SmoothStep<POS, WIDTH>
```

# Arguments
POS, WIDTH: FUNCTION
return value: FUNCTION
POS: specifies the middle of the smoothstep, 0 = base of blade, 32768=tip
WIDTH: witdth of transition, 0 = no transition, 32768 = length of blade
Example: SmoothStep<Int<16384>, Int<16384>> returns 0 up until 25% of the blade.

# Description
From there it has a smooth transition to 32768, which will be reached at 75% of
the blade. If WIDTH is negative, the transition will go the other way.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/smoothstep.h#L4
