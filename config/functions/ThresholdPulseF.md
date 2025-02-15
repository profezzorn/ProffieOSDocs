---
title: ThresholdPulseF
---

# Usage
```cpp
ThresholdPulseF&lt;F, THRESHOLD, HYST_PERCENT&gt;
```

# Arguments
F: FUNCTION
THRESHOLD: FUNCTION (defaults to Int<32768>)
HYST_PERCENT: FUNCTION (defaults to Int<66>

# Description
Returns 32768 once when F > THRESHOLD, then waits until
F < THRESHOLD * HYST_PERCENT / 100 before going back
to the initial state (waiting for F > THRESHOLD).

# See Also
[IncrementModulo](/config/functions/IncrementModulo.html), [IncrementF](/config/functions/IncrementF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/increment.h#L40
