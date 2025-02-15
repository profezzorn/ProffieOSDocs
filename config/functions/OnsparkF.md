---
title: OnsparkF
---

# Usage
```cpp
OnsparkF<MILLIS>
```

# Arguments
MILLIS: FUNCTION (defaults to Int<200>)
return value: FUNCTION

# Description
When the blade turns on, this function starts returning
32768, then fades back to zero over MILLIS milliseconds.
This is intended to be used with Mix<> or AlphaL<> to
to create a flash of color or white when the blade ignites.

# See Also
[Mix](/config/styles/Mix.html), [AlphaL](/config/styles/AlphaL.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/on_spark.h#L4
