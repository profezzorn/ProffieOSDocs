---
title: TrJoin
---

# Usage
```cpp
TrJoin<TR1, TR2, ...>
```

# Arguments
 * TR1, TR2: TRANSITION
 * return value: TRANSITION

# Description
A little hard to explain, but all the specified
transitions are run in parallel. Basically, we
chain transitions like ((A TR1 B) TR2 B)

# See Also
[TrJoinR](/config/transitions/TrJoinR.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/join.h#L4
