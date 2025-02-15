---
title: Lockup
redirect_from:
  - /config/styles/LockupL.html
---

# Usage
```cpp
Lockup&lt;BASE, LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE&gt;
LockupL&lt;LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE, LB_SHAPE&gt;
```

# Arguments
BASE, LOCKUP: COLOR
DRAG_COLOR: COLOR (defaults to the LOCKUP color)
LOCKUP_SHAPE: FUNCTION (defaults to Int<32768>)
DRAG_SHAPE: FUNCTION (defaults to SmoothStep<Int<28671>, Int<4096>>)
LB_SHAPE: FUNCTION (defaults to a suitable function)
return value: COLOR

# Description
Shows LOCKUP if the lockup state is true, otherwise BASE.
Also handles Drag, Melt and Lightning Block lockup types unless those
are handled elsewhere in the same style.

# See Also
[LockupTr](/config/styles/LockupTr.html), [SmoothStep](/config/functions/SmoothStep.html), [IsLessThan](/config/functions/IsLessThan.html), [LayerFunctions](/config/functions/LayerFunctions.html), [Scale](/config/functions/Scale.html), [BrownNoiseF](/config/functions/BrownNoiseF.html), [SlowNoise](/config/functions/SlowNoise.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/lockup.h#L25
