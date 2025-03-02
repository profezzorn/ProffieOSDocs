---
title: SubBladeWithList
---
ProffieOS has several subblade variants, for different arrangement of pixels. But if your pixel arrangement doesn't match any of those, then you should use SubBladeWithList, as it lets you specify exactly which pixels are a part of the subblade, and in any order.

## SubBladeWithList example:

```cpp
SubBladeWithList<0,10,1,9>(blade_definition)
```

This will create a blade out of the first, 11th, 2nd and 10th pixel, in that order.


See also: [SubBlade](/config/blades/subblade.html), [SubBladeReverse](/config/blades/subbladereverse.html), [SubBladeZZ](/config/blades/subbladezz.html), [SubBladeWithStride](/config/blades/subbladewithstride.html)
