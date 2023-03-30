---
title: How to set up a blaster
---

#Blaster Setup HOW-TO

## Introduction
If you want to setup a blaster, first you have to understand the general mechanics of the `blaster.h` prop. A blaster is always on (unless a dedicated Power button is added). The `blaster.h` prop offers three "modes": Stunt, Kill and Auto. Also, you have a certain number of shots until you need to reload. And you have a certain chance of your weapon randombly jamming.

## Hardware
We will assume for exposition purposes that you will be using a Proffie V2.2 board. You will have two buttons, a WS2812B strip on the weapon barrel, powered by LED 2 (pin 19), plus a Red LED for an accent powered by LED 4 (pin 5). You will connect your Fire button (trigger) to Button1 (pin 21) and your Mode button (selector) to Button2 (pin 23). Optionally, you can connect either a Power button, or a Clip Detect switch to Button3 (pin 22), and of course an OLED.

## Soundfonts
You will need at least one blaster soundfont. There are some free soundfonts only a search away.

### List of Names and Effects
| Filename | Effect |
|---|---|
| `bgnauto` | Played when auto fire starts |
| `auto` | Played while auto fire is
| `endauto` | Played when auto fire ends |
| `blast` |
| `boot` | Played when ProffieOS boots up. |
| `clipin` | Sound made when inserting a clip |
| `clipout` | Sound made when dropping a clip |
| `empty` | Sound when the weapon is out of rounds |
| `fire` | Firing sound |
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

*If `mdkill`, `mdstun`, `mdauto` nor `mode` are present Talkie voice speaks selected mode.*

### OLED Animations
[TODO]

## Configuration
Then comes the time to configure the board's `config.h`. You should start by adding to your `CONFIG_TOP` section the following defines

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
#define BLASTER_SHOTS_UNTIL_EMPTY 15  // The capacity of your weapons rounds.
#define BLASTER_JAM_PERCENTAGE 1     //  0-100. If not defined, random.

#endif
```

So, you will start by setting the `CONFIG_PROP` to use the `blaster.h` prop.

```
/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PROP

#include "../props/blaster.h"

#endif
```

You can then add your Presets to `CONFIG_PRESETS`:

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

BladeConfig blades[] = {
 { 10000,
   WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2> >(),,
   SimpleBladePtr<CreeXPE2RedTemplate<1000>, NoLED, NoLED, NoLED, bladePowerPin4, -1, -1, -1>(),
   CONFIGARRAY(presets) },
};

#endif
```

And last you should set your `CONFIG_BUTTONS` defines:

```
#ifdef CONFIG_BUTTONS
Button FireButton(BUTTON_FIRE, powerButtonPin, "fire");
Button ModeButton(BUTTON_MODE_SELECT, auxPin, "modeselect");
//Button PowerButton(BUTTON_POWER, aux2Pin, "power"); //A third button to power on/off your weapon
//Button PowerButton(BUTTON_CLIP_DETECT, aux2Pin, "clip"); //A third button is a clip sensor. It should be closed when the clip is in, and open when the clip is removed. 
#endif
```

## Config example

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
//Button PowerButton(BUTTON_CLIP_DETECT, aux2Pin, "clip"); //A third button is a clip sensor. It should be closed when the clip is in, and open when the clip is removed. 
#endif
```
