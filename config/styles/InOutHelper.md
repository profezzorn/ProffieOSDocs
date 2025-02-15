---
title: InOutHelper
---

# Usage
```cpp
InOutHelper&lt;BASE, OUT_MILLIS, IN_MILLIS&gt;
InOutHelper&lt;BASE, OUT_MILLIS, IN_MILLIS, OFF_COLOR&gt;
```

# Arguments
BASE, OFF_COLOR: COLOR
OUT_MILLIS, IN_MILLIS: a number
return value: COLOR

# Description
This class does a basic extend/retract. Basically it fades between
BASE and OFF_COLOR (which defaults to black). It starts by just
displaying OFF_COLOR, and when you turn the saber on it starts mixing
in BASE at the base of the saber. After OUT_MILLIS milliseconds, it
will be displaying the BASE color on the entire blade.

# See Also
[InOutHelperX](/config/styles/InOutHelperX.html), [InOutTr](/config/styles/InOutTr.html), [AlphaL](/config/styles/AlphaL.html), [Layers](/config/styles/Layers.html), [Ifon](/config/functions/Ifon.html), [InOutFunc](/config/functions/InOutFunc.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/inout_helper.h#L25
