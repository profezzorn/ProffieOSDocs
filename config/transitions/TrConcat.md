---
title: TrConcat
---

# Usage
```cpp
TrConcat&lt;TRANSITION, INTERMEDIATE, TRANSITION, ...&gt;
```

# Arguments
OR:  TrConcat<TRANSITION, TRANSITION, ...>
TRANSITION: TRANSITION
INTERMEDIATE: COLOR
return value: TRANSITION

# Description
Concatenates any number of transitions.
If an intermediate color is provided, we first transition to that color, then
we transition away from it in the next transition.
If no intermediate color is provided, the first and second transition will both
transition from the same input colors. If for instance both the first and second
transitions are TrFades, then there will be a jump in the middle as the transition
will go back and start from the beginning. Using TimeReverseX on the second transition
will avoid this, as the second transition will then run backwards.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/concat.h#L4
