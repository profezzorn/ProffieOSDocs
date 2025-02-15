---
title: IncrementModulo
---

# Usage
```cpp
IncrementModulo&lt;PULSE, MAX, INCREMENT&gt;
```

# Arguments
PULSE: FUNCTION (pulse type)
MAX: FUNCTION (not zero) defaults to Int<32768>
INCREMENT: FUNCTION defaults to Int<1>

# Description
Increments by I each time PULSE occurs wraps around when
it reaches MAX.

# See Also
[ThresholdPulseF](/config/functions/ThresholdPulseF.html), [IncrementF](/config/functions/IncrementF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/increment.h#L6
