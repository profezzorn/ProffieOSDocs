---
title: IncrementWithReset
---

# Usage
```cpp
IncrementWithReset&lt;PULSE, RESET_PULSE, MAX, I&gt;
```

# Arguments
PULSE: FUNCTION (pulse type)
RESET_PULSEE: FUNCTION (pulse type) defaults to Int<0> (no reset)
MAX, I: FUNCTION

# Description
Starts at zero, increments by I each time the PULSE occurse.
If it reaches MAX it stays there.
Resets back to zero when RESET_PULSE occurs.

# See Also
[EffectPulse](/config/functions/EffectPulse.html), [LockupPulseF](/config/functions/LockupPulseF.html), [EffectIncrementF](/config/functions/EffectIncrementF.html), [IncrementModulo](/config/functions/IncrementModulo.html), [ThresholdPulseF](/config/functions/ThresholdPulseF.html), [IncrementF](/config/functions/IncrementF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/effect_increment.h#L48
