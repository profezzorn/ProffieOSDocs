---
title: LockupTr
redirect_from:
  - /config/styles/LockupTrL.html
---

# Usage
```cpp
LockupTr&lt;BASE, COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION&gt;
LockupTrL&lt;COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION&gt;
```

# Arguments
COLOR: COLOR or LAYER
BeginTr, EndTr: TRANSITION
LOCKUP_TYPE: a SaberBase::LockupType
Return type: LAYER

# Description
This layer creates a complete lockup effect.
When lockup is initiated, BeginTr is used to transition from transparent
to COLOR. When lockup ends, EndTr is used to transition from COLOR to
transparent again. If you wish to for your lockup to have a shape, you
can have COLOR be partially transparent to make the base layer show through.
If CONDITION equals 0, Lockup effect ignored

# See Also
[Lockup](/config/styles/Lockup.html), [SmoothStep](/config/functions/SmoothStep.html), [IsLessThan](/config/functions/IsLessThan.html), [LayerFunctions](/config/functions/LayerFunctions.html), [Scale](/config/functions/Scale.html), [BrownNoiseF](/config/functions/BrownNoiseF.html), [SlowNoise](/config/functions/SlowNoise.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/lockup.h#L103
