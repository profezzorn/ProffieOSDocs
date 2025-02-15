---
title: InOutHelperX
---

# Usage
```cpp
InOutHelperX<BASE, EXTENSION, OFF_COLOR>
```

# Arguments
BASE, OFF_COLOR: COLOR
EXTENSION: FUNCTION
return value: COLOR

# Description
This class does a basic extend/retract. Basically it fades between
BASE and OFF_COLOR (which defaults to black). The amount of extension
is determined by EXTENSION. If EXTENSION returns 32768, the blade is fully
extended. If it returns zero, it is not extended.

# See Also
[InOutHelper](/config/styles/InOutHelper.html), [InOutTr](/config/styles/InOutTr.html), [AlphaL](/config/styles/AlphaL.html), [Layers](/config/styles/Layers.html), [Ifon](/config/functions/Ifon.html), [InOutFunc](/config/functions/InOutFunc.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/inout_helper.h#L10
