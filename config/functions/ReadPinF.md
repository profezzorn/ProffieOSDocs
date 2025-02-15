---
title: ReadPinF
---

# Usage
```cpp
ReadPinF&lt;PIN&gt;
ReadPinF&lt;PIN, PIN_MODE&gt;
```

# Arguments
PIN: int, pin you want your style to respond to
PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT

# Description
returns INTEGER, 0 if pin is low and 32768 if pin is high

# See Also
[AnalogReadPinF](/config/functions/AnalogReadPinF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/readpin.h#L6
