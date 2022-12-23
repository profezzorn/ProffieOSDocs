dual_prop.h allows for 2 discrete prop files to be used, 
alternating on a latched switch (Blade Detect).   
This is useful when you want a saber to 
toggle to a blaster for example, 
and you want the buttons to take on different behaviors.

How to: Use the following lines where you set your prop file in your config.
```
#ifdef CONFIG_PROP   
#include "../props/dual_prop.h"   
#include "../props/saber_sa22c_buttons.h"   
#include "../props/blaster.h"   
#undef PROP_TYPE   
#define PROP_TYPE DualProp<SaberSA22CButtons, Blaster>   
#endif   
```
** Note the prop file SaberSA22CButtons here would change
to the file name of the prop you choose.

Then setup your config file for 2 states:
Bladein preset bank, and a BladeOut preset bank.   
Give the BladeConfig 2 sets of descriptions, and
#define BLADE_DETECT_PIN properly.

Read more about blade detect here:
https://github.com/profezzorn/ProffieOS/wiki/Blade-Detect