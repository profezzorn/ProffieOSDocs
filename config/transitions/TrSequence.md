---
title: TrSequence
---

# Usage
```cpp
TrSequence<TR1, TR2, ...>
```

# Arguments
TR1, TR2: TRANSITION
return value: TRANSITION

# Description
Each time a new transition is started, a transition is selected
sequentially, such that the frist time a transition is started
TR1 will be selected, then TR2, etc.
When the end of the sequence is reached, the next transition selected
wraps back around to TR1.

# See Also
[TrRandom](/config/transitions/TrRandom.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/sequence.h#L6
