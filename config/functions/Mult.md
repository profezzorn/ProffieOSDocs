---
title: Mult
---

# Usage
```cpp
Mult&lt;F, V&gt;
```

# Arguments
F, V: FUNCTION
return value: FUNCTION

# Description
Fixed point multiplication of values F * V,
fixed point 16.15 arithmetic (32768 = 1.0)
(2*2 would not result in 4),
(16384 * 16384 = 8192, representation of 0.5*0.5=0.25)
most blade functions use this method of fixed point calculations

# See Also
[Percentage](/config/functions/Percentage.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/mult.h#L4
