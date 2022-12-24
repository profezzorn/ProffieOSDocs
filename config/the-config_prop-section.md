---
title: The CONFIG_PROP section
---
The CONFIG_PROP section is relatively new, and a lot of config files don't use it. The purpose of the CONFIG_PROP section is to specify which class is given control of what everything does. Most of the time, this is done by simply including a file from the ProffieOS/props directory in your config file, like this:

    #ifdef CONFIG_PROP
    #include "../props/detonator.h"
    #endif

However, it would be perfectly fine to define your own prop class in this section and then define PROP_CLASS to be the name of your class.  Learning how to do that is outside the scope of this tutorial though.

Here is a list of prop files that come with ProffieOS, each file will have some additional instructions at the top.

* [saber.h](https://github.com/profezzorn/ProffieOS/blob/master/props/saber.h) - this is the default, you don't need a CONFIG_PROP section to use this.
* [saber_sa22c_buttons.h](https://github.com/profezzorn/ProffieOS/blob/master/props/saber_sa22c_buttons.h) - saber prop with button assignments designed by sa22c.
* [saber_shtok_buttons.h](https://github.com/profezzorn/ProffieOS/blob/master/props/saber_shtok_buttons.h) - saber prop with button assignments designed by Dmitry Shtok.
* [saber_fett263_buttons.h](../props/fett263/battle-mode-os5.md) - saber prop with button assignments designed by fett263, includes battle mode.
* [saber_BC_buttons.h](https://github.com/profezzorn/ProffieOS/blob/master/props/saber_BC_buttons.h) - (ProffieOS 6 or later) saber prop with button assignments and features designed by Brian Conner.
* [detonator.h](https://github.com/profezzorn/ProffieOS/blob/master/props/detonator.h) - thermal detonator prop.
* [blaster.h](https://github.com/profezzorn/ProffieOS/blob/master/props/blaster.h) - blaster prop.
* [audiofx.h](https://github.com/profezzorn/ProffieOS/blob/master/props/audiofx.h) - similar to an adafruit audiofx board.
* [micom.h](https://github.com/profezzorn/ProffieOS/blob/master/props/micom.h) - voice/dialog prop.
