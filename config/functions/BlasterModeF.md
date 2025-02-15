---
title: BlasterModeF
---

# Usage
```cpp
BlasterModeF
```

# Arguments
Returns the current blaster mode as an integer:

# Description
0 for MODE_STUN, 1 for MODE_KILL, 2 for MODE_AUTO
This function should only be used when BLASTER_SHOTS_UNTIL_EMPTY is defined,
indicating that the current prop is a Blaster.
Example usage in a style for Blue Stun, Red Kill, and Green Auto:
StylePtr<ColorSelect<BlasterModeF, TrInstant, Blue, Red, Green>>()

# See Also
[StylePtr](/config/styles/StylePtr.html), [ColorSelect](/config/styles/ColorSelect.html), [TrInstant](/config/transitions/TrInstant.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/blaster_mode.h#L6
