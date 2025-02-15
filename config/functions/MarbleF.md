---
title: MarbleF
---

# Usage
```cpp
MarbleF<OFFSET, FRICTION, ACCELERATION, GRAVITY>
```

# Arguments
OFFSET: FUNCTION  0-32768, adjust until "down" represents is actually down
FRICTION: FUNCTION, higher values makes the marble slow down, usually a constant
ACCELERATION: FUNCTION, a function specifying how much speed to add to the marble
GRAVITY: FUNCTION higher values makes the marble heavier
return value: FUNCTION  0-32768, representing point on a circle

# Description
This is intended for a small ring of neopixels.
It runs a simulation of a marble trapped in a circular
track and returns the position of that marble.
Meant to be used with CircularSectionF to turn the marble
position into a lighted up section.

# See Also
[CircularSectionF](/config/functions/CircularSectionF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/marble.h#L6
