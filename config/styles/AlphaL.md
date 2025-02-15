---
title: AlphaL
---

# Usage
```cpp
AlphaL<COLOR, ALPHA>
```

# Arguments
 * COLOR: COLOR or LAYER
 * ALPHA: FUNCTION
 * Return value: LAYER

# Description
This function makes a color transparent. The ALPHA function specifies just how opaque it should be.
If ALPHA is zero, the returned color will be 100% transparent. If Alpha is 32768, the returned color will
be 100% opaque. Note that if COLOR is already transparent, it will be made more transparent. Example:
If COLOR is 50% opaque, and ALPHA returns 16384, the result will be 25% opaque.

# See Also
[Mix](/config/styles/Mix.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/alpha.h#L6
