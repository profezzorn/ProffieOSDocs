---
title: TrLoopUntil
---

# Usage
```cpp
TrLoopUntil<PULSE, TRANSITION, OUT>
```

# Arguments
TRANSITION, OUT: TRANSITION
PULSE: FUNCTION (pulse)
Return Value: TRANSITION

# Description
Runs the specified transition until the pulse occurs.
When the pulse occurs, the loop continues, but OUT is used to
transition away from it, and when OUT is done, the transition is done.

# See Also
[TrLoop](/config/transitions/TrLoop.html), [TrLoopNX](/config/transitions/TrLoopNX.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/loop.h#L52
