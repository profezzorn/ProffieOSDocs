---
title: LayerFunctions
---

# Usage
```cpp
LayerFunctions&lt;F1, F2, ...&gt;
```

# Arguments
F1, F2: FUNCTIONS
return value: FUNCTION

# Description
Returns (32768 - (32768 - F1) * (32768 * F2) / 32768)
This is the same as 1-(1-F1)*(1-F2), but multiplied by 32768.
Basically Mix<LayerFunctions<F1, F2>, A, B> is the same as Mix<F2, Mix<F1, A, B>, B>.

# See Also
[Mix](/config/styles/Mix.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/layer_functions.h#L4
