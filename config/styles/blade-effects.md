---
title: Blade Style EFFECTs
---

Events of animations on the blade are triggered by various things.  
Some examples are ignition, clash, blast, etc...  
When these are triggered by a button event, a gesture, or other means, the way the blade knows which animation, or EFFECT to show, is by designating it in the blade style.  
A basic example:
```cpp
TransitionEffectL<TrConcat<TrWipe<50>,White,TrWipe<50>>,EFFECT_BLAST>
```
In plain English, this says "When I press the blaster deflect button, run a string of concatenated events that wipe White for 50ms, then wipe it away."  
Any EFFECT can be substituted in place of the EFFECT_BLAST argument above.  
Note that some of these EFFECTS may be included in features used by some prop files (button controls files) but not in others.

The majority of these are self explanitory. 
Just read EFFECT as "do something during_XXXX"
### EFFECT_NONE  
### EFFECT_CLASH  
### EFFECT_BLAST  
### EFFECT_FORCE  
### EFFECT_STAB  
### EFFECT_BOOT  
### EFFECT_LOCKUP_BEGIN  
### EFFECT_LOCKUP_END  
### EFFECT_DRAG_BEGIN  
### EFFECT_DRAG_END  
### EFFECT_PREON  
### EFFECT_POSTOFF  
### EFFECT_IGNITION  
### EFFECT_RETRACTION  

### EFFECT_CHANGE  
When using color change.  

### EFFECT_NEWFONT  
Used when changing presets.  

### EFFECT_LOW_BATTERY  

### EFFECT_POWERSAVE  
Typically used to apply a dimming effect on blade to conserve battery.

### EFFECT_BATTERY_LEVEL  
Show battery level visually on blade.  

### EFFECT_FAST_ON  
When using a feature that skips preon.  

## Blaster effects  
### EFFECT_STUN  
### EFFECT_FIRE  
### EFFECT_CLIP_IN  
### EFFECT_CLIP_OUT  
### EFFECT_RELOAD  
### EFFECT_MODE  
### EFFECT_RANGE  
### EFFECT_EMPTY  
### EFFECT_FULL  
### EFFECT_JAM  
### EFFECT_UNJAM  
### EFFECT_PLI_ON  
### EFFECT_PLI_OFF  

## User-definable effects  
### EFFECT_USER1  
### EFFECT_USER2  
### EFFECT_USER3  
### EFFECT_USER4  

## ----- The following are as of ProffieOS7 -----

### EFFECT_VOLUME_LEVEL    
Show volume level visually on blade, great for using with volume menu feature.  

### EFFECT_QUOTE  
### EFFECT_SECONDARY_IGNITION  
### EFFECT_SECONDARY_RETRACTION  
### EFFECT_OFF  

### EFFECT_FAST_OFF  
When using a feature that bypasses postoff.  

### EFFECT_OFF_CLASH  
### EFFECT_NEXT_QUOTE  
### EFFECT_INTERACTIVE_PREON  
### EFFECT_INTERACTIVE_BLAST  
### EFFECT_TRACK  
### EFFECT_BEGIN_BATTLE_MODE  
### EFFECT_END_BATTLE_MODE  
### EFFECT_BEGIN_AUTO_BLAST  
### EFFECT_END_AUTO_BLAST  

### EFFECT_ALT_SOUND  
Triggers the change for sets of sounds within the font from one alternative to another.  

### EFFECT_TRANSITION_SOUND  
Triggers an optional sound effect during transitions from within a style via TrDoEffect.  

### EFFECT_SOUND_LOOP  
Toggles an optonal sound effect loop ON/OFF from within a style via TrDoEffect.  

## Mini game effects  
### EFFECT_GAME_START  
### EFFECT_GAME_ACTION1  
### EFFECT_GAME_ACTION2  
### EFFECT_GAME_CHOICE  
### EFFECT_GAME_RESPONSE1  
### EFFECT_GAME_RESPONSE2  
### EFFECT_GAME_RESULT1  
### EFFECT_GAME_RESULT2  
### EFFECT_GAME_WIN  
### EFFECT_GAME_LOSE  

## User-definable effects  
### EFFECT_USER5  
### EFFECT_USER6  
### EFFECT_USER7  
### EFFECT_USER8
