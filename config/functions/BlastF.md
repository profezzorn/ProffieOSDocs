---
title: BlastF
---

# Usage
```cpp
BlastF&lt;FADEOUT_MS, WAVE_SIZE, WAVE_MS, EFFECT&gt;
```

# Arguments
FADOUT_MS: a number (defaults to 200)
WAVE_SIZE: a number (defaults to 100)
WAVE_MS: a number (defaults to 400)
EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)
returned value: FUNCTION

# Description
This function is intended to be used in a Mix<> or AlphaL<>
When a blast occurs, it makes a wave starting at the blast
location (which is currently random) and travels out
from that direction. At the peak, this function returns
32768 and when there is no blast it returns zero.
The FADOUT_MS controls how long it takes the wave to
fade out. The WAVE_SIZE controls the width of the wave.
The WAVE_MS parameter controls the speed of the waves.
EFFECT can be used to trigger this effect by something
other than a blast effect.

# See Also
[BlastFadeoutF](/config/functions/BlastFadeoutF.html), [OriginalBlastF](/config/functions/OriginalBlastF.html), [Mix](/config/styles/Mix.html), [AlphaL](/config/styles/AlphaL.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/blast.h#L4
