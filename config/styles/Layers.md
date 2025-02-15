---
title: Layers
---

# Usage
```cpp
Layers<BASE, LAYER1, LAYER2, ...>
```

# Arguments
BASE: COLOR or LAYER
LAYER1, LAYER2: LAYER
return value: COLOR or LAYER (same as BASE)

# Description
This style works like layers in gimp or photoshop.
In most cases, the layers are expected to be normally transparent effects
that turn opaque when then want to paint an effect over the base color.
If the base color is opqaque, the final result of this style will also be
opaque. If the base color is transparent, the final result may also be transparent,
depending on what the layers paint on top of the base color.

# See Also
[AlphaL](/config/styles/AlphaL.html), [Int](/config/functions/Int.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/layers.h#L8
