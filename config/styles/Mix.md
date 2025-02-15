---
title: Mix
---

# Usage
```cpp
Mix&lt;F, A, B&gt;
Mix&lt;F, A, B, C, ....&gt;
```

# Arguments
F: INTEGER
A, B, C: COLOR
return value: COLOR or LAYER (if A or B is a layer)

# Description

Mix between A and B using function F
F = 0 -> return A
F = 16384 -> return (A+B)/2
F = 32768 -> return B

With 3 arguments (or more), Mix between A, B and C using function F
F = 0 -> return A
F = 1 -> mostly A, a little B
F = 2 -> a little more A, a little less B
F = 32767 -> mostly last color, a little of the last-but-one color
F = 32768 -> last color

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/mix.h#L8
