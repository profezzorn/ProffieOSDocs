---
title: TransitionLoop
redirect_from:
  - /config/styles/TransitionLoopL.html
---

# Usage
```cpp
TransitionLoop<COLOR, TRANSITION>
TransitionLoopL<TRANSITION>
```

# Arguments
 * COLOR: COLOR
 * TRANSITION : TRANSITION
 * return value: COLOR

# Description

Continuously transitions COLOR to COLOR  
Makes more sense if TRANSITION is a TrConcat, as this will  
transition to/from the intermediate steps in a loop.

# Usage
```cpp
TransitionLoopWhileL<LOOP_TRANSITION, END_TRANSITION, CONDITION>
TransitionLoopL<TRANSITION>
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
[TrConcat](/config/transitions/TrConcat.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/transition_loop.h#L4
