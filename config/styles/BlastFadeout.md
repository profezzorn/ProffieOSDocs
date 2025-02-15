---
title: BlastFadeout
redirect_from:
  - /config/styles/BlastFadeoutL.html
---

# Usage
```cpp
BlastFadeout<BASE, BLAST, FADEOUT_MS>
BlastFadeoutL<BLAST, FADEOUT_MS>
```

# Arguments
 * BASE, BLAST: COLOR
 * FADEOUT_MS: a number (defaults to 250)
 * return value: COLOR

# Description
Normally shows BASE, but swiches to BLAST when a blast
is requested and then fades back to BASE. FADEOUT_MS
specifies out many milliseconds the fade takes.

# See Also
[Blast](/config/styles/Blast.html), [OriginalBlast](/config/styles/OriginalBlast.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/blast.h#L20
