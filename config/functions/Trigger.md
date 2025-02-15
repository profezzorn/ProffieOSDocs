---
title: Trigger
---

# Usage
```cpp
Trigger&lt;EFFECT, FADE_IN_MILLIS, SUSTAIN_MILLIS, FADE_OUT_MILLIS, DELAY&gt;
```

# Arguments
EFFECT: BladeEffectType
FADE_IN_MILLIS: INTEGER
SUSTAIN_MILLIS: INTEGER
FADE_OUT_MILLIS: INTEGER
DELAY_MILLIS: INTEGER (defaults to Int<0>)
return value: INTEGER

# Description
Normally returns 0, but when EFFECT occurs, it ramps up to 32768,
stays there for SUSTAIN_MILLIS, then fades down to zero again.
If delay is specified, the whole thing is delayed that much before it starts.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/trigger.h#L4
