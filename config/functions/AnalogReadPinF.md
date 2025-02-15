---
title: AnalogReadPinF
---

# Usage
```cpp
AnalogReadPinF<PIN>
AnalogReadPinF<PIN, PIN_MODE>
```

# Arguments
PIN: int, pin you want your style to respond to
PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT

# Description
returns INTEGER, 0-32768 depending on input reading.
Notes:
* May cause slowdowns
* may not update every run() call
* pin modes other than INPUT may not be supported,
* Only analog-capable pins will work.

# See Also
[ReadPinF](/config/functions/ReadPinF.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/readpin.h#L28
