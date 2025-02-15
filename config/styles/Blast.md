---
title: Blast
redirect_from:
  - /config/styles/BlastL.html
---

# Usage
```cpp
Blast<BASE, BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>
BlastL<BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>
```

# Arguments
BASE, BLAST: COLOR
FADEOUT_MS: a number (defaults to 150)
WAVE_SIZE: a number (defaults to 100)
WAVE_MS: a number (defaults to 400)
return value: COLOR

# Description
Normally shows BASE, but creates a blast effect using
the color BLAST when a blast is requested. The effect
is basically two humps moving out from the blast location.
The size of the humps can be changed with WAVE_SIZE, note
that smaller values makes the humps bigger. WAVE_MS determines
how fast the waves travel. Smaller values makes the waves
travel slower. Finally FADEOUT_MS determines how fast the
humps fade back to the base color.

# See Also
[BlastFadeout](/config/styles/BlastFadeout.html), [OriginalBlast](/config/styles/OriginalBlast.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/blast.h#L4
