---
title: How to set up a blaster
---

# Introduction
If you want to setup a blaster, first you have to understand the general mechanics of the `blaster.h` prop. A blaster is always on (unless a dedicated Power button is added). The `blaster.h` prop offers three "modes": Stunt, Kill and Auto. Also, you have a certain number of shots until you need to reload. And you have a certain chance of your weapon randombly jamming.

# Hardware
You will need a ProffieOS compatible board, at least two momentary buttons and at least one LED to illuminate each fire action, plus a speaker.
Please note that button behaviour differs from the saber props. As such you can have Fire (required), Mode (required), Power, Reload, Clip and/or Range. Most are of momentary type, except Clip that can be latching. Both for momentary and latching switches when it is closed a clip is assumed to be in, while open is assumed as a Clip not present.
Speaker is handled exactly the same as in the saber version, and so are the blades. The main difference is that in your hardware installation you will probably use fixed illumination elements rather than removable ones.
For exposition purposes we will assume that you will be using a Proffie V2.2 board. Also, you will have two buttons, a WS2812B strip on the weapon barrel, powered by LED 2 (pin 19), plus a Red LED for an accent powered by LED 4 (pin 5). You will connect your Fire button (trigger) to Button1 (pin 21) and your Mode button (selector) to Button2 (pin 23). Optionally, you can connect a Power button, a Reload or a Clip switch (pin 22, TX, blade3Pin, or other), and of course an OLED.
If you are not installing a Power button, be advise that you need to have a `poweron01.wav` file in your soundfont or the blaster will default to starting turned off and you will have no method to turn it on.
In the particular case of Clip, it will consider that it has a clip while the circuit is closed and that the clip has been removed when the circuit is open. Thus, if you just want the button, you should use a latching switch. If you have a physical clip with a sensor of the clip's presence, then a momentary switch might work, too.

# Soundfonts
You will need at least one blaster soundfont. There are some free soundfonts only a search away. Please pay attention whether you have a `poweron` file in all your fonts if you don't have a Power button.

## List of Names and Effects
| Filename | Effect |
|---|---|
| `bgnauto` | Played when auto fire starts. |
| `auto` | Played while auto fire is going. |
| `endauto` | Played when auto fire ends. |
| `blast` | Is the semi-automatic fire sound. You can have as many as you want. |
| `boot` | Played when ProffieOS boots up. |
| `clipin` | Sound made when inserting a clip. |
| `clipout` | Sound made when dropping a clip. |
| `empty` | Sound when the weapon is out of rounds. |
| `font` | Name of the preset. |
| `full` | Sound made when the weapon is full of ammo. |
| `hum` | Constant sound looping while not firing. |
| `jam` | Sound made when the weapon jam.s |
| `unjam` | Sound made when unjamming the blaster. |
| `mode` | Sound made when switching mode (OS 6+: when `mdkill`, `mdstun` and/or `mdauto` not present) |
| `plioff` | Played while retracting the PLI bargraph. | 
| `plion` | Played while extending the PLI bargraph. |
| `poweron` | If this file is present, the blaster will start once it is turned on. If not, *you will need a Power button to power it on*. |
| `range` |  Sounds of increasing weapon range/power. Currently not implemented. |
| `stun` | Firing sound for stun mode. |
| `reload` | Reloading sound. |
| `mdkill` | (OS 6+) Sound made when switching to KILL mode |
| `mdstun` | (OS 6+) Sound made when switching to STUN mode |
| `mdauto` | (OS 6+) Sound made when switching to AUTO mode |

*If no `mdkill`, `mdstun`, `mdauto` nor `mode` are present Talkie voice speaks selected mode.*

# OLED Animations
[TODO]

# Configuration
Then comes the time to configure the board's `config.h`. Proffieboard uses the same hardware and OS for blasters, thermal detonators and blasters. Thus, we will assume you are somewhat familiar with the saber configuration. If you find defines or elements that are not documented here, they are probably documented on the saber side. We will provide links to the relevant sections of the define for a more complete explanation.
So, we will propose a sample config for the hardware that we proposed as an example, and then we will go over the particulars of the blaster define.

## Configuration Sample

```
/****** CONFIG_TOP blaster defines  ****/
#ifdef CONFIG_TOP

#include "proffieboard_v2_config.h"
#define NUM_BLADES 2    // We use a WS2812B LED string for the barrel, plus a straight red LED for an accent.
#define NUM_BUTTONS 2   // First button is fire, second adds Mode Select, you can add Power, Reload or Clip Detect.
                        // As always, you have to add them in `CONFIG_BUTTONS`.
const unsigned int maxLedsPerStrip = 144;
#define CLASH_THRESHOLD_G 2.0         //Affects the shaking for unjamming your weapon.
#define VOLUME 1500                   // 0-3000 usual range. Don't overload your speaker.

// Stock required defines
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD

//OLED Specific
//#define ENABLE_SSD1306		            //To enable stock 128x32 monochrome SSD1306 OLED
//#define INCLUDE_SSD1306               //To enable a different aspect ratio, needs some further configuration.

//Blaster specific.
#define ENABLE_BLASTER_AUTO          // If you desire to enable AUTO mode.
#define BLASTER_SHOTS_UNTIL_EMPTY 15 // The capacity of your weapons rounds.
#define BLASTER_JAM_PERCENTAGE 1     //  0-100. If not defined, random.


#endif

/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PROP

#include "../props/blaster.h"

#endif

/****** CONFIG_PROP blaster defines  ****/
#ifdef CONFIG_PRESETS

Preset presets[] = {
	// Default basic blast color with red audio flicker on blast
	{ "blaster/E-11",
		"tracks/mars.wav",
		StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Blue>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
		StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
	  "E-11"
	},
  // Different prop with audio flicker and a simple color for the accent.
	{ "blaster/E-11D",
		"blaster/E-11D/tracks/EzraTheme.wav",
		StylePtr<Layers<AudioFlicker<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,128>>>,BlastL<White>, InOutTrL<TrInstant,TrFade<300>,Pulsing<RotateColorsX<Variation,Blue>,RotateColorsX<Variation,Rgb<0,0,10>>,3000>>>>(),
		StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
		"E-11D"
	}
};

BladeConfig blades[] = {
 { 10000,
   WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2> >(),
   SimpleBladePtr<CreeXPE2RedTemplate<1000>, NoLED, NoLED, NoLED, bladePowerPin4, -1, -1, -1>(),
   CONFIGARRAY(presets) },
};

#endif

#ifdef CONFIG_BUTTONS
Button FireButton(BUTTON_FIRE, powerButtonPin, "fire");
Button ModeButton(BUTTON_MODE_SELECT, auxPin, "modeselect");
//Button PowerButton(BUTTON_POWER, aux2Pin, "power"); //A third button to power on/off your weapon
//Button ClipButton(BUTTON_CLIP_DETECT, blade4Pin, "clip"); //Actually clip sensor. It should be closed when the clip is in, and open when the clip is removed. So you can use either latching as single button or momentary if it is a physical clip inserted sensor.
//Button ReloadButton(BUTTON_RELOAD, blade3Pin, "reload"); //Dedicated button for reloading.

#endif

/*** OS 7+
#ifdef CONFIG_STYLES
using BasicRedBlastWithBlueStunAndAudioFlicker = StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Blue>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>;
// Add to preset as: StylePtr<BasicRedBlastWithBlueStunAndAudioFlicker>()
#endif
*/
```

## CONFIG_TOP Section
In the `CONFIG_TOP` section the following defines are the specifics for defining your weapon. For the rest of the defines please consult the [CONFIG_TOP documentation](config/the-config_top-section.html).

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

## CONFIG_PROP Section
This section is currently trivial as `blaster.h` is the only currently available prop for blaster use.

## CONFIG_PRESETS Section
Here we have really two different sets of definitions: your `Preset` which define your soundfont and styles used, and the `BladeConfig` which define your hardware.
For the presets syntax and definition you should consult de [preset configuration](config/preset-configuration.html), and probably familiarize yourself with the [styles configuration](config/styles/blade-styles.html). Please note that you can have multiple presets, like `presetneopixel[]` , `presetnoblade[]`, etc.
For the blades section, the [CONFIG_PRESETS documentation](config/the-config_presets-section.html) is a good introduction. And for most of needs, understanding the [WS281XBladePtr](config/blades/ws281xbladeptr.html) and the [SimpleBladePtr](config/blades/simplebladeptr.html) should sufice. If you want to be able to dynamically change your hardware, you should read the [Blade ID section](howto/blade-id.html).

For this example, we defined two different presets: `E-11` and `E-11D`. Please note that in the preset:
```
	{ "blaster/E-11",
		"tracks/mars.wav",
		StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Blue>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
		StylePtr<Lockup<BlastFadeout<BlastFadeout<Black,AudioFlicker<Black,Red>,250,EFFECT_FIRE>,AudioFlicker<Black,Red>,1500,EFFECT_STUN>,AudioFlicker<Black,Red>>>(),
	  "E-11"
	},
```
The `"blaster/E-11D"` line is the folder which contains your soundfont. The `"tracks/mars.wav"` is the background music track, and here `tracks/mars.wav` is pointing to a `tracks` folder on your SD card's root. If you want to use a track in your soundfont's folder you will need to put the full path like `"blaster/E-11D/tracks/mars.wav"`. For the style definition, you need one for each blade you have defined in `NUM_BLADES` in the `CONFIG_TOP` section, and will be assigned in the order you defined in the `BladeConfig` definition.
Also we defined two different "blades":
```
BladeConfig blades[] = {
 { 10000,
   WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2> >(),
   SimpleBladePtr<CreeXPE2RedTemplate<1000>, NoLED, NoLED, NoLED, bladePowerPin4, -1, -1, -1>(),
   CONFIGARRAY(presets) },
};
```
The first blade is a 108 pixel WS2812B string, while the second blade is a single Cree led with a 1000 mOhms resistor.

## CONFIG_BUTTONS
Then you should set your `CONFIG_BUTTONS`. As we said before, you really want a bare minimum of two buttons: Fire and Mode. But you can add Power, Reload and Clip dedicated buttons. As stated before, we assume mostly momentary buttons for Fire, Mode, Power and Reload. But for Clip if you just want a button, you should use a latching button that will simulate a clip in while closed and out when open. If you have physical clip with a detection mechanism, you can use a momentary button.
Since most boards only have 3 button pads, you can use any of blade2Pin, blade3Pin, blade4Pin, blade5Pin or blade6Pin. For other model of boards, you should consult the specific documentation on the extra pins.

## CONFIG_STYLES
From OS 7.x onwards, the `CONFIG_STYLES` section has been added. It allows you to put your styles definition here and then simply call the function from the `CONFIG_PRESET` as you can read in the [CONFIG_STYLES documentation](config/the-config_styles-section.html). It allows to call the same function in the Prop section many times, even with different arguments. This makes a cleaner config and saver memory by not repeating similar styles.

# Blaster Use
## Single Button
**Buttons**: *FIRE*
This case quite limited since you can only fire. Weapon will always be on the default mode (STUN is the defined in the prop, if you wish another you will have to change it on the code). Weapon will always be powered on *but you need a `poweron.wav` file present or the blaster will default to off and you will not have a switch to turn it on*. And if you have limited amount of rounds you can't reload.

* Fire -                  Click *FIRE*. (Hold to Auto Fire / Rapid Fire if you have `ENABLE_BLASTER_AUTO`)
* Unjam -                 Bang the blaster.

## Dual Button
**Buttons**: *FIRE* and *MODE*

This is the "stock" configuration. Weapon will always start on the default mode (STUN is the defined in the prop, if you wish another you will have to change it on the code). Weapon will always be powered on *but you need a `poweron.wav` file present or the blaster will default to off and you will not have a switch to turn it on*.

* Fire -                  Click *FIRE*. (Hold to Auto Fire / Rapid Fire if you have `ENABLE_BLASTER_AUTO`)
* Cycle Modes -           Click *MODE*.
* Next Preset -           Long click and release *MODE*.
* Previous Preset -       Double click and hold *MODE*, release after a second.
* Reload -                Hold *MODE* until Reloaded. (Or Click Reload if dedicated button insatlled)
* Start/Stop Track -      Double click *MODE*.
* Unjam -                 Bang the blaster.

## Additional Buttons
**Button**: *POWER*, *CLIP*, *RELOAD*
### POWER
* Power On / Off -        Click *POWER*.

### CLIP
* Clip In -               *CLIP* pad Latched On. ( or Hold if Momentary button)
* Clip out -              *CLIP* pad Latched Off. ( or release if Momentary button)

### RELOAD
* Reload -                Hold *RELOAD* until Reloaded.
