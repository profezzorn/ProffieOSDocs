---
title: "ColorChange<> in a blade style"
redirect_from:
  - /color-change-modes.html
---
The template is `ColorChange<TRANSITION, COLOR1, COLOR2, ...>`   
ProffieOS will detect if the style uses ColorChange<> or not.  
If it does NOT use ColorChange<>, the "color wheel" will be activated, which has 32768 steps per rotation.  
If it does contain ColorChange<>, the OS will let the ColorChange<> template handle the change. When you activate color change mode, there will be up to 12 steps per rotation with a little sound at each step (ccchange.wav)  
The prop file used will determine the button combinations to Enter and Exit Color Change mode, as well as save a chosen color, or Exit without changing anything.  

IF the style uses ColorChange<>, AND you have `#define COLOR_CHANGE_DIRECT` in your config file, then when you activate color change mode, it will immediately go to the next color with the button press and exit color change mode. 
If the style does not use ColorChange<>, having `#define COLOR_CHANGE_DIRECT` active has no effect.

# **RotateColorsX<Variation,COLOR>**
If you use this in a blade style, the "color wheel" colorchange will only affect the colors in a RotateColorsX, and the other colors will not change.
This is useful if you want your base blade color to change, but leave all of the effects like clash, blast, lockup etc... unchanged.
It is also a good way to prevent other blade's styles in the preset (like an accent LED) from changing with the main blade.
If you want to prevent ANY color change on a style, you could just insert a single ColorChange<> value, like `ColorChange<TrInstant,Blue>`, or make a non-changing Black or White to be `RotateColorsX<Variation,Black>`  

## Disable Color Change
If you want to completely disable any color change option, you can use the following define in [The CONFIG_TOP section](/config/the-config_top-section.html) of the config file.
```cpp
#define DISABLE_COLOR_CHANGE
```

