---
title: TrJoinR
---

# Usage
```cpp
TrJoinR<TR1, TR2, ...>
```

# Arguments
TR1, TR2: TRANSITION
return value: TRANSITION

# Description
Similar to TrJoin, but transitions are chained
to the right instead of to the left. Like:
(A TR2 (A TR1 B))

# See Also
[TrJoin](/config/transitions/TrJoin.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/join.h#L32
