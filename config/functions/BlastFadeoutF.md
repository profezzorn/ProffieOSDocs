---
title: BlastFadeoutF
---

# Usage
```cpp
BlastFadeoutF<FADEOUT_MS, EFFECT>
```

# Arguments
FADEOUT_MS: a number (defaults to 250)
EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)
return value: FUNCTION

# Description
NOrmally returns 0, but returns up to 32768 when the
selected effect occurs. Then if fades back to zero over
FADEOUT_MS milliseconds.

# See Also
[BlastF](/config/functions/BlastF.html), [OriginalBlastF](/config/functions/OriginalBlastF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/blast.h#L69
