---
title: EffectPosition
---

# Usage
```cpp
EffectPosition<>
EffectPosition<EFFECT>
```

# Arguments
 * EFFECT: effect type
 * return value: INTEGER

# Description

EffectPosition returns the position of a particular effect. 0 = base, 32768 = tip.
For now, this location is random, but may be set explicitly in the future.
When used as EffectPosition<> inside a TransitionEffectL whose EFFECT is already specified,
then it will automatically use the right effect.

# See Also
[TransitionEffect](/config/styles/TransitionEffect.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/effect_position.h#L4
