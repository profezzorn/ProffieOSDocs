---
title: EffectIncrementF
---

# Usage
```cpp
EffectIncrementF&lt;EFFECT, MAX, I&gt;
```

# Arguments
I, MAX: FUNCTION
return value: FUNCTION

# Description
Increases by value I (up to MAX) each time EFFECT is triggered
If current value + I = MAX, it returns 0.
If adding I exceeds MAX, the function returns 0 + any remainder in excesss of MAX

# See Also
[EffectPulse](/config/functions/EffectPulse.html), [LockupPulseF](/config/functions/LockupPulseF.html), [IncrementWithReset](/config/functions/IncrementWithReset.html), [IncrementModulo](/config/functions/IncrementModulo.html), [ThresholdPulseF](/config/functions/ThresholdPulseF.html), [IncrementF](/config/functions/IncrementF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/effect_increment.h#L88
