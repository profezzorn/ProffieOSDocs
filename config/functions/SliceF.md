---
title: SliceF
---

# Usage
```cpp
SliceF&lt;DENSITY_FUNCTION&gt;
SliceF&lt;DENSITY_FUNCTION, OFFSET&gt;
```

# Arguments
DENSITY_FUNCTION: 3DF
OFFSET: integer, defaults to 20
return value: FUNCTION

# Description
The DENSITY_FUNCTION is a 3-dimensional function, f(x, y, z)
the SliceF function calculates the x/y/z coordinates based on the
angle of the blade. For now, the only density functions available
are SmokeDF and FastSmokeDF, which are basically the same thing.
This is very similar to how the POV blade works, but instead of
using a large data blob as input, it just uses another function
as input.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/slice.h#L4
