---
title: WavLen
---

# Usage
```cpp
WavLen&lt;&gt;
WavLen&lt;EFFECT&gt;
```

# Arguments
EFFECT: effect type
return value: INTEGER

# Description

WavLen (length of wav file) takes the duration of a wav file sound
and can be used to replace time integer arguments in a blade style.
Example: TrFadeX<WavLen<EFFECT_RETRACTION>>
When used as WavLen<> inside a TransitionEffectL whose EFFECT is already specified,
then it will automatically use the right effect.
Example: TransitionEffectL<TrConcat<TrWipex<WavLen<>>,White,TrWipeX<WavLen<>>>,EFFECT_BLAST>

# See Also
[TrFadeX](/config/transitions/TrFadeX.html), [TransitionEffect](/config/styles/TransitionEffect.html), [TrConcat](/config/transitions/TrConcat.html), [TrWipeX](/config/transitions/TrWipeX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/wavlen.h#L4
