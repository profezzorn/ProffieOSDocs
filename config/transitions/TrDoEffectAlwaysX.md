---
title: TrDoEffectAlwaysX
redirect_from:
  - /config/transitions/TrDoEffectsAlways.html
---

# Usage
```cpp
TrDoEffectAlwaysX&lt;TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS&gt;
TrDoEffectsAlways&lt;TRANSITION, EFFECT, WAVNUM, LOCATION&gt;
```

# Arguments
TRANSITION: TRANSITION
EFFECT: effect type
WAVNUM, LOCATION: a number
LOCATION_CLASS: INTEGER
return value: TRANSITION

# Description
TrDoEffectAlways is the same as TrDoEffectX, but runs even if
the blade is off.

# See Also
[TrDoEffectX](/config/transitions/TrDoEffectX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/doeffect.h#L19
