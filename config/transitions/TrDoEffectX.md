---
title: TrDoEffectX
redirect_from:
  - /config/transitions/TrDoEffect.html
---

# Usage
```cpp
TrDoEffectX<TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS>
TrDoEffect<TRANSITION, EFFECT, WAVNUM, LOCATION>
```

# Arguments
TRANSITION: TRANSITION
EFFECT: effect type
WAVNUM, LOCATION: a number
LOCATION_CLASS: INTEGER
return value: TRANSITION

# Description
Runs the specified TRANSITION and triggers EFFECT (unless the blade is off)
Can specify WAV file to use for EFFECT with WAVNUM
NOTE: 0 is first wav file, -1 is random wav
LOCATION = -1 is random

# See Also
[TrDoEffectAlwaysX](/config/transitions/TrDoEffectAlwaysX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/doeffect.h#L7
