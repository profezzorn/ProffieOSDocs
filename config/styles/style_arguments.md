---
title: Style Arguments
---

Styles in ProffieOS can use arguments to make them more useful. Arguments can be integers or colors that can be changed by using the edit mode, or the ProffieOS workbench. There are two style templates that make this possible:

```cpp
RgbArg<ARGUMENT_NUMBER, DEFAULT_COLOR>
or
IntArg<ARGUMENT_NUMBER, DEFALUT_VALUE>
```

While you don't have to use these arguments, they can be very useful for saving memory and making your saber or prop more dynamic and configurable.

Let's consider a simple preset, and I want a red, a green, and a blue preset, I would do:

```cpp
{"font1", "tracks/track1.wav",
 StylePtr<EasyBlade<Red, White, 800, 300>>(),
 "label"},
{"font2", "tracks/track2.wav",
 StylePtr<EasyBlade<Green, White, 800, 300>>(),
 "label"},
{"font3", "tracks/track3.wav",
 StylePtr<EasyBlade<Blue, White, 800, 300>>(),
 "label"},
```

Not a problem, right? Since these are simple styles, they won't take up much space, and because they were made without arguments, they cannot be modified at run time.

Using arguments, I could instead write this as a single preset:
```cpp
{"font1", "tracks/track1.wav",
 StylePtr<EasyBlade<RgbArg<BASE_COLOR_ARG, Red>, White, 800, 300>>(),
 "label"},
```

Then I could use edit mode or the ProffieOS workbench to copy this preset two more times, and change the fonts and the color for each preset. These copies would not take up any extra FLASH memory, which means I can use that memory for something else. (Like more styles...)

From ProffieOS 7.x, this gets even better, because you can specify the default arguments in the config file, like this:
```cpp
{"font1", "tracks/track1.wav",
 StylePtr<EasyBlade<RgbArg<BASE_COLOR_ARG, Red>, White, 800, 300>>("65535,0,0"),
 "label"},
{"font2", "tracks/track2.wav",
 StylePtr<EasyBlade<RgbArg<BASE_COLOR_ARG, Red>, White, 800, 300>>("0,65535,0"),
 "label"},
{"font3", "tracks/track3.wav",
 StylePtr<EasyBlade<RgbArg<BASE_COLOR_ARG, Red>, White, 800, 300>>("0,0,65535"),
 "label"},
```
**Note the use of Rgb16 values*  

Because were using the very same style each time, it doesn't actually use up any more memory, and we don't have to use the style editor or the proffieos workbench to do the edits. It can all be done in the config file. Also, if we mess something up using edit mode, we can delete presets.ini and presets.tmp from the SD card, without losing the defaults.

If you don't know what string to put between the parenthesis, you can use edit mode/workbench to configure it the way you want it, then open up presets.ini/tmp and check the strings saved in there, then copy them to the config file.

By convention, these are the arguments we normally use in proffieos:
* BASE_COLOR_ARG = 1, // Primary Base Color
* ALT_COLOR_ARG = 2, // Alternate or Force Color (free-use)
* STYLE_OPTION_ARG = 3, // Style Option
* IGNITION_OPTION_ARG = 4, // Ignition Options
* IGNITION_TIME_ARG = 5, // used in IgnitionTime alias
* IGNITION_DELAY_ARG = 6, // Ignition Delay Time                                                                                                           
* IGNITION_COLOR_ARG = 7, // Ignition "Power Up" Color
* IGNITION_POWER_UP_ARG = 8, // Ignition "Power Up" Options
* BLAST_COLOR_ARG = 9, // Blast Color
* CLASH_COLOR_ARG = 10, // Clash Color
* LOCKUP_COLOR_ARG = 11, // Lockup Color
* LOCKUP_POSITION_ARG = 12, // Clash/Lockup Location for Responsive Effects (mid-point)
* DRAG_COLOR_ARG = 13, // Drag Color
* DRAG_SIZE_ARG = 14, // Drag Size
* LB_COLOR_ARG = 15, // Lightning Block Color
* STAB_COLOR_ARG = 16, // Stab / Melt Color
* MELT_SIZE_ARG = 17, // Stab / Melt Size
* SWING_COLOR_ARG = 18, // Swing Color (Responsive Swing Effects)
* SWING_OPTION_ARG = 19, // Swing Options (Responsive Swing Effects)
* EMITTER_COLOR_ARG = 20, // Emitter Color (Emitter Spark) can be used for PostOff
* EMITTER_SIZE_ARG = 21, // Emitter Size (Emitter Spark), can be used for PostOff
* PREON_COLOR_ARG = 22, // PreOn Color
* PREON_OPTION_ARG = 23, // PreOn Option
* PREON_SIZE_ARG = 24, // PreOn Size
* RETRACTION_OPTION_ARG = 25, // Retraction Options
* RETRACTION_TIME_ARG = 26, // used in RetractionTime alias
* RETRACTION_DELAY_ARG = 27, // Retraction Delay Time
* RETRACTION_COLOR_ARG = 28, // Retraction "Cool Down" Color
* RETRACTION_COOL_DOWN_ARG = 29, // Retraction "Cool Down" Options
* POSTOFF_COLOR_ARG = 30, // PostOff Color
* OFF_COLOR_ARG = 31, // Off Color (Color when blade is Off for crystals and accents)
* OFF_OPTION_ARG = 32, // Off Options (when blade is Off, for crystals and accents)
* ALT_COLOR2_ARG = 33, // Generic 2nd Alt Color
* ALT_COLOR3_ARG = 34, // Generic 3rd Alt Color
* STYLE_OPTION2_ARG = 35, // Generic 2nd Style Option
* STYLE_OPTION3_ARG = 36, // Generic 3rd Style Option
* IGNITION_OPTION2_ARG = 37, // Ignition BEND Option
* RETRACTION_OPTION2_ARG = 38, // Retraction BEND Option                                        

Note that this is just convetion. You *can* use IntArg<1, 1> in your style if you want to, but it will probably not work correctly with edit mode and the workbench.

