---
title: How to set up a blaster
---

# Introduction
If you want to setup a blaster, first you have to understand the general mechanics of the `blaster.h` prop. A blaster is always on (unless a dedicated Power button is added). The `blaster.h` prop offers three "modes": Stunt, Kill and Auto. Also, you have a certain number of shots until you need to reload. And you have a certain chance of your weapon randombly jamming.

# Hardware
You will need a ProffieOS compatible board, at least two momentary buttons and at least one LED to illuminate each fire action, plus a speaker.
Please note that button behaviour differs from the saber props. As such you can have Fire (required), Mode (required), Power, Reload, Clip and/or Range. Most are of momentary type, except Clip that can be latching. Both for momentary and latching switches when it is closed a clip is assumed to be in, while open is assumed as a Clip not present.
Speaker is handled exactly the same as in the saber version, and so are the blades. The main difference is that in your hardware installation you will probably use fixed illumination elements rather than removable ones.
For exposition purposes we will assume that you will be using a Proffie V2.2 board. Also, you will have two buttons, a WS2812B strip on the weapon barrel, powered by LED 2 (pin 19), plus a Red LED for an accent powered by LED 4 (pin 5). You will connect your Fire button (trigger) to Button1 (pin 21) and your Mode button (selector) to Button2 (pin 23). Optionally, you can connect either a Power button,a Reload or a Clip switch to Button3 (pin 22), and of course an OLED.

# Soundfonts
You will need at least one blaster soundfont. There are some free soundfonts only a search away.

## List of Names and Effects
| Filename | Effect |
|---|---|
| `bgnauto` | Played when auto fire starts |
| `auto` | Played while auto fire is |
| `endauto` | Played when auto fire ends |
| `blast` | Is the semi-automatic fire sound. You can have as many as you want |
| `boot` | Played when ProffieOS boots up. |
| `clipin` | Sound made when inserting a clip |
| `clipout` | Sound made when dropping a clip |
| `empty` | Sound when the weapon is out of rounds |
| `fire` | Currently does nothing |
| `font` | Name of the preset |
| `full` | Sound made when the weapon is full of ammo |
| `hum` | Constant sound looping while not firing |
| `jam` | Sound made when the weapon jams |
| `unjam` | Sound made when unjamming the blaster |
| `mode` | Sound made when switching mode (OS 6+: when `mdkill`, `mdstun` and/or `mdauto` not present) |
| `plioff` | Played while retracting the PLI bargraph. | 
| `plion` | Played while extending the PLI bargraph. |
| `range` |  Up to 16 sounds of increasing weapon range/power |
| `stun` | Firing sound for stun mode |
| `reload` | Reloading sound |
| `mdkill` | (OS 6+) Sound made when switching to KILL mode |
| `mdstun` | (OS 6+) Sound made when switching to STUN mode |
| `mdauto` | (OS 6+) Sound made when switching to AUTO mode |

*If no `mdkill`, `mdstun`, `mdauto` nor `mode` are present Talkie voice speaks selected mode.*

# OLED Animations
[TODO]

# Configuration
Then comes the time to configure the board's `config.h`. In the `CONFIG_TOP` section the following defines are important for defining your weapon. The rest might still be valid.

## Required Defines

### NUM_BLADES
Similarly to the saber version, each "blade" is a string of pixels (or a single one) that will have a styled defined for each soundfont. Remember that any accent, crystal chamber and subblade you define counts towards a different blade.

```cpp
#define NUM_BLADES 2
```

### NUM_BUTTONS
And we must also specify how many buttons we have. Remember that for `blaster.h` prop, your first button is Fire, the second is Mode button and then you can add Power, Reload or Clip.

```cpp
#define NUM_BUTTONS 2
```

### CLASH_THRESHOLD_G
This sets the sensibility when you have to bang your weapon to unjamm it.

```cpp
#define CLASH_THRESHOLD_G 2.0
```

### VOLUME
Then we specify the volumes. Generally values between 0 and 3000 are useful, but it may depend on what kind of board you have.

```cpp
#define VOLUME 1500
```

### Standard Features
Finally, we have a set of defines that enable standard features.
It's on my TODO list to make these not required:

```cpp
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD
```

## Optional Defines

### ENABLE_BLASTER_AUTO
This define determines if your weapon has the automatic fire mode enabled. If you want your weapon to be semi-automatic only, simply comment it out.
```cpp
#define ENABLE_BLASTER_AUTO
```

### BLASTER_SHOTS_UNTIL_EMPTY
This is your weapon round capacity per "clip" (i.e. before needing to reload). If you want an infinite ammo weapon, simply comment it out.
```cpp
#define BLASTER_SHOTS_UNTIL_EMPTY 15
```

### BLASTER_JAM_PERCENTAGE
Here we set the change of the weapon jamming per shot. The range is 0-100. Please note that if you comment it out, it will be replaced with a random chance per ignition.
```cpp
#define BLASTER_JAM_PERCENTAGE 1
```

## Config Sections Samples

### CONFIG_TOP

For the `CONFIG_TOP` section we will adjust it for the hardware we had assumed in our hardware section.

```
/****** CONFIG_TOP blaster defines  ****/
#ifdef CONFIG_TOP

#include "proffieboard_v2_config.h"
#define NUM_BLADES 2    // Weapon barrel plus the accent
#define NUM_BUTTONS 2   // First button is fire, second adds Mode Select and third is either Power or Clip Detect.
                        // As always, you have to add them in `CONFIG_BUTTONS`.
const unsigned int maxLedsPerStrip = 144;
#define CLASH_THRESHOLD_G 2.0         //Affects the shaking for unjamming your weapon.
#define VOLUME 1500
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD
#define ENABLE_BLASTER_AUTO           // If you desire to enable AUTO mode.
#define BLASTER_SHOTS_UNTIL_EMPTY 15  // The capacity of your weapons rounds. Comment to have infinite ammo.
#define BLASTER_JAM_PERCENTAGE 3     //  0-100. If not defined, random.

#endif
```

### CONFIG_PROP
So, you will start by setting the `CONFIG_PROP` to use the `blaster.h` prop. It currently is the only prop adjusted for blaster use.

```
/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PROP

#include "../props/blaster.h"

#endif
```

### CONFIG_PRESET

You can then add your Presets to `CONFIG_PRESETS`. In this case we defined two different presets: one for E-11 and another for E-11D. Also, please note that for using different colors on FIRE and STUN mode, it should be done inside the style. Then again, for the monochromatic LED, you can't do anything but control the output power, so take that into consideration for your styles.

```
/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PRESETS

Preset presets[] = {
// Default basic blast color with red audio flicker on blast
{ "E-11", "tracks/mars.wav",
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Blue>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>() },
  "E-11" },
{ "E-11D", "tracks/EzraTheme.wav",
  StylePtr<Layers<AudioFlicker<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,128>>>,BlastL<White>, InOutTrL<TrInstant,TrFade<300>,Pulsing<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,10>>,3000>>>>(),
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>() },
  "E-11D" }
;
```

Defining your blades is exactly the same as for a saber. You can use [SubBlades](/config/blades/subblade.html) and even use [Blade ID](/howto/blade-id.html) and [Blade Detect](/howto/blade-detect.html). If you are using LED please read [this page](/config/blades/led-configuration.html).
```
BladeConfig blades[] = {
 { 10000,
   WS281XBladePtr<40, bladePin, Color8::GRB, PowerPINS<bladePowerPin2> >(),,
   SimpleBladePtr<CreeXPE2RedTemplate<1000>, NoLED, NoLED, NoLED, bladePowerPin4, -1, -1, -1>(),
   CONFIGARRAY(presets) },
};

#endif
```

### CONFIG_BUTTONS

And last you should set your `CONFIG_BUTTONS`. As we said before, you need a bare minimum of two buttons: Fire and Mode. But you can add Power, Reload and Clip dedicated buttons.

```
#ifdef CONFIG_BUTTONS
Button FireButton(BUTTON_FIRE, powerButtonPin, "fire");
Button ModeButton(BUTTON_MODE_SELECT, auxPin, "modeselect");
//Button PowerButton(BUTTON_POWER, aux2Pin, "power"); //A third button to power on/off your weapon
//Button ClipButton(BUTTON_CLIP_DETECT, aux2Pin, "clip"); //Actually clip sensor. It should be closed when the clip is in, and open when the clip is removed. So you can use either latching or momentary.
//Button ReloadButton(BUTTON_RELOAD, aux2Pin, "reload"); //Dedicated button for reloading.
//Button RangeButton(BUTTON_RANGE, aux2Pin, "reload"); //Dedicated button for increasing range/power of the weapon.

#endif
```

## Complete Config example

```
/****** CONFIG_TOP blaster defines  ****/
#ifdef CONFIG_TOP

#include "proffieboard_v2_config.h"
#define NUM_BLADES 2
#define NUM_BUTTONS 2   // First button is fire, second adds Mode Select and third is either Power or Clip Detect.
                        // As always, you have to add them in `CONFIG_BUTTONS`.
const unsigned int maxLedsPerStrip = 144;
#define CLASH_THRESHOLD_G 2.0         //Affects the shaking for unjamming your weapon.
#define VOLUME 1500
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD
#define ENABLE_BLASTER_AUTO          // If you desire to enable AUTO mode.
#define BLASTER_SHOTS_UNTIL_EMPTY 15 // The capacity of your weapons rounds.
#define BLASTER_JAM_PERCENTAGE 1     //  0-100. If not defined, random.
#define ENABLE_SSD1306		           //To enable OLED

#endif

/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PROP

#include "../props/blaster.h"

#endif

/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PRESETS

Preset presets[] = {
// Default basic blast color with red audio flicker on blast
{ "E-11", "tracks/mars.wav",
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Blue>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>() },
  "E-11" },
{ "E-11D", "tracks/EzraTheme.wav",
  StylePtr<Layers<AudioFlicker<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,128>>>,BlastL<White>, InOutTrL<TrInstant,TrFade<300>,Pulsing<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,10>>,3000>>>>(),
  StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>() },
  "E-11D" }
;

BladeConfig blades[] = {
 { 10000,
   WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2> >(),,
   SimpleBladePtr<CreeXPE2RedTemplate<1000>, NoLED, NoLED, NoLED, bladePowerPin4, -1, -1, -1>(),
   CONFIGARRAY(presets) },
};

#endif

#ifdef CONFIG_BUTTONS
Button FireButton(BUTTON_FIRE, powerButtonPin, "fire");
Button ModeButton(BUTTON_MODE_SELECT, auxPin, "modeselect");
//Button PowerButton(BUTTON_POWER, aux2Pin, "power"); //A third button to power on/off your weapon
//Button ClipButton(BUTTON_CLIP_DETECT, aux2Pin, "clip"); //Actually clip sensor. It should be closed when the clip is in, and open when the clip is removed. So you can use either latching or momentary.
//Button ReloadButton(BUTTON_RELOAD, aux2Pin, "reload"); //Dedicated button for reloading.
//Button RangeButton(BUTTON_RANGE, aux2Pin, "reload"); //Dedicated button for increasing range/power of the weapon.

#endif
```

# Blaster Use

## Single Button

**Buttons**: *FIRE*

This case quite limited since you can only fire. Weapon will always be on the default mode (STUN is the defined in the prop, if you wish another you will have to change it on the code). Weapon will always be powered on. And if you have limited amount of rounds you can't reload.

* Fire -                  Click *FIRE*. (Hold to Auto Fire / Rapid Fire if you have `ENABLE_BLASTER_AUTO`)
* Unjam -                 Bang the blaster.

## Dual Button

**Buttons**: *FIRE* and *MODE*

This is the "stock" configuration. Weapon will always start on the default mode (STUN is the defined in the prop, if you wish another you will have to change it on the code). Weapon will always be powered on.

* Fire -                  Click *FIRE*. (Hold to Auto Fire / Rapid Fire if you have `ENABLE_BLASTER_AUTO`)
* Cycle Modes -           Click *MODE*.
* Next Preset -           Long click and release *MODE*.
* Previous Preset -       Double click and hold *MODE*, release after a second.
* Reload -                Hold *MODE* until Reloaded. (Or Click Reload if dedicated button insatlled)
* Start/Stop Track -      Double click *MODE*.
* Unjam -                 Bang the blaster.

## Additional Buttons

**Button**: *POWER*, *CLIP*, *RELOAD*, *RANGE*

### POWER
* Power On / Off -        Click *POWER*.

### CLIP
* Clip In -               *CLIP* pad Latched On. ( or Hold if Momentary button)
* Clip out -              *CLIP* pad Latched Off. ( or release if Momentary button)

### RELOAD
* Reload -                Hold *RELOAD* until Reloaded.

### RANGE

While the button and the font for this event are defined, `blaster.h` does not currently handle them.

