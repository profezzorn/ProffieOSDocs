---
title: StylePtr
---

# Usage
```cpp
StylePtr<BLADE>
```

# Arguments
BLADE: COLOR
return value: suitable for preset array

# Description
Most blade styls are created by taking a blade style template and wrapping it
this class, which implements the BladeStyle interface. We do this so that the
getColor calls will be inlined in this loop for speed.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/style_ptr.h#L6
