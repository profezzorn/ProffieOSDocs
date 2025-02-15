---
title: TimeSinceEffect
---

# Usage
```cpp
TimeSinceEffect<>
TimeSinceEffect<EFFECT>
```

# Arguments
 * EFFECT: effect type
 * return value: INTEGER

# Description

TimeSinceEffect returns the number of milliseconds since a particular
effect occured.
When used as TimeSinceEffect<> inside a TransitionEffectL whose EFFECT is already specified,
then it will automatically use the right effect.

# See Also
[TransitionEffect](/config/styles/TransitionEffect.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/time_since_effect.h#L4
