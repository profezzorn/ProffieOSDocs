---
title: Percentage
---

# Usage
```cpp
Percentage&lt;F, V&gt;
```

# Arguments
F: FUNCTION
V: INTEGER
return value: FUNCTION

# Description
Gets Percentage V of value F,
Percentages over 100% are allowed and will effectively be a multiplier.
example Percentage<Int<16384>,25>
this will give you 25% of Int<16384> and returns Int<4096>

# See Also
[Mult](/config/functions/Mult.html), [Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/mult.h#L51
