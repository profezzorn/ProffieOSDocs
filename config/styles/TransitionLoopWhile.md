---
title: TransitionLoop
redirect_from:
  - /config/styles/TransitionLoopL.html
---

# Usage
```cpp
TransitionLoopWhileL<LOOP_TRANSITION, END_TRANSITION, CONDITION>
```

# Arguments
 * LOOP_TRANSITION : TRANSITION
 * END_TRANSITION : TRANSITION
 * CONDITION: FUNCTION
 * return value: COLOR

# Description

Continuously runs LOOP_TRANSITION while CONDITION > 0  
Makes more sense if TRANSITION is a TrConcat, as this will  
transition to/from the intermediate steps in a loop.  
If CONDITION <= 0, runs END_TRANSITION and stops.

# See Also
[TransitionLoop](/config/styles/TransitionLoop.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/5def63b4b75c8cc9aa8ae761a8ae10a3d1e59992/styles/transition_loop.h#L49
