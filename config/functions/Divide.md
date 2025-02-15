---
title: Divide
---

# Usage
```cpp
Divide<F, V>
```

# Arguments
F, V: FUNCTION,
return value: FUNCTION

# Description
Divide F by V
If V = 0, returns 0
Please note that Divide<> isn't an exact inverse of Mult<> because mult uses fixed-point mathematics
(it divides the result by 32768) while Divide<> doesn't, it just returns F / V

# See Also
[Mult](/config/functions/Mult.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/divide.h#L4
