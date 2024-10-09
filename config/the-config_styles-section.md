---
title: The CONFIG_STYLES section
---

Please note, the CONFIG_STYLES section requires ProffieOS 7.x or later.

The CONFIG_STYLES section is a convenience location for placing custom style templates and aliases in your config file. In ProffieOS 6.x and older, you would need to put these sort of statements in the CONFIG_PRESETS section, somewhere before the presets[] array. While this is still entirely possible, it can be inconvenient, because the styles are often large and unchanging, while the presets may be tweaked a lot more often. By putting the styles in their own section, we now have the option of putting them anywhere we want in the config file, since sections can be written in any order. Normally, the CONFIG_STYLES section is expected to be near the bottom of the config file.

Here is an example of what it could look like:
```cpp
#ifdef CONFIG_STYLES
using BatteryLevelStyle = InOutHelperX<Gradient<Red,Orange,Yellow,Green,Green,Green,Green>, BatteryLevel>;
#endif
```

Please not that there is no actual difference between putting things at the top of the CONFIG_PRESETS section and putting them in the CONFIG_STYLES section, it is merely provided make it easier to keep your config file organized.
