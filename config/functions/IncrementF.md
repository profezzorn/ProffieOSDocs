---
title: IncrementF
---

# Usage
```cpp
IncrementF<F, V, MAX, I, HYST_PERCENT>
```

# Arguments
F, V, I, MAX: FUNCTION
HYST_PERCENT: FUNCTION percent (defaults to 66)
return value: FUNCTION

# Description
Increases by value I (up to MAX) each time F >= V
Detection resets once F drops below V * HYST_PERCENT
if greater than MAX returns 0

# See Also
[IncrementModulo](/config/functions/IncrementModulo.html), [ThresholdPulseF](/config/functions/ThresholdPulseF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/increment.h#L82
