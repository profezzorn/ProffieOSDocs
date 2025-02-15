---
title: TransitionEffect
redirect_from:
  - /config/styles/TransitionEffectL.html
---

# Usage
```cpp
TransitionEffect<COLOR, EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>
TransitionEffectL<EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>
```

# Arguments
COLOR, EFFECT_COLOR: COLOR
TRANSITION1, TRANSITION2 : TRANSITION
EFFECT: effect type
return value: COLOR

# Description

When the specified EFFECT happens (clash/blast/etc.) transition from COLOR to
EFFECT_COLOR using TRANSITION1. Then transition back using TRANSITION2.

# See Also
[TrConcat](/config/transitions/TrConcat.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/transition_effect.h#L6
