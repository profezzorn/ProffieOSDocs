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

- [General effects](#general-effects)
- [Blaster effects](#blaster-effects)
- [Mini game effects](#mini-game-effects)
- [User-definable effects](#user-definable-effects)
- [Errors](#errors)


## General effects
### EFFECT_NONE
Never generated, used as defaults in some places to mean "no effect", but is otherwise not useful for anything.
### CLASH_UPDATE
*(OS 6.0+)* No effect in blade styles, but may be used in props and other places to detect when the strength of a clash increases after the EFFECT_CLASH has occurred..

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
*(OS 6.0+)* 

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

### EFFECT_ON
*(OS 7.0+)*

### EFFECT_OFF
*(OS 7.0+)*

### EFFECT_FAST_ON  
When using a feature that skips preon.

### EFFECT_FAST_OFF
*(OS 7.0+)* When using a feature that bypasses postoff.  

### EFFECT_VOLUME_LEVEL
*(OS 7.0+)* Show volume level visually on blade, great for using with volume menu feature.  

### EFFECT_QUOTE
*(OS 7.0+)* 

### EFFECT_SECONDARY_IGNITION
*(OS 7.0+)* 

### EFFECT_SECONDARY_RETRACTION
*(OS 7.0+)* 

### EFFECT_OFF_CLASH
*(OS 7.0+)* 

### EFFECT_NEXT_QUOTE
*(OS 7.0+)* 

### EFFECT_INTERACTIVE_PREON
*(OS 7.0+)* 

### EFFECT_INTERACTIVE_BLAST
*(OS 7.0+)* 

### EFFECT_TRACK
*(OS 7.0+)* 

### EFFECT_BEGIN_BATTLE_MODE
*(OS 7.0+)* 

### EFFECT_END_BATTLE_MODE
*(OS 7.0+)* 

### EFFECT_BEGIN_AUTO_BLAST
*(OS 7.0+)* 

### EFFECT_END_AUTO_BLAST
*(OS 7.0+)* 

### EFFECT_ALT_SOUND
*(OS 7.0+)* Triggers the change for sets of sounds within the font from one alternative to another.  
See: [Alt Sounds](/sound/alt_sounds.html)
### EFFECT_TRANSITION_SOUND
*(OS 7.0+)* Triggers an optional sound effect during transitions from within a style via TrDoEffect.  
Basic usage example:  
`TrDoEffect<CURRENT_TRANSITION,EFFECT_TRANSITION_SOUND>`  
Uses sounds named trNN.wav, where N is a number if more than one tr.wav exist.  

### EFFECT_SOUND_LOOP
*(OS 7.0+)* Toggles an optonal sound effect loop ON/OFF from within a style via TrDoEffect.  
Used like a user-defined Lockup state in coordination with a control and visual effect.  
Uses sounds named trloopNN.wav, where N is a number if more than one trloop.wav exist.

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

## Mini game effects  
### EFFECT_GAME_START
*(OS 7.0+)* 

### EFFECT_GAME_ACTION1
*(OS 7.0+)* 

### EFFECT_GAME_ACTION2
*(OS 7.0+)* 

### EFFECT_GAME_CHOICE
*(OS 7.0+)* 

### EFFECT_GAME_RESPONSE1
*(OS 7.0+)* 

### EFFECT_GAME_RESPONSE2
*(OS 7.0+)* 

### EFFECT_GAME_RESULT1
*(OS 7.0+)* 

### EFFECT_GAME_RESULT2
*(OS 7.0+)* 

### EFFECT_GAME_WIN
*(OS 7.0+)* 

### EFFECT_GAME_LOSE
*(OS 7.0+)* 


## User-definable effects  
### EFFECT_USER1
### EFFECT_USER2
### EFFECT_USER3
### EFFECT_USER4
### EFFECT_USER5
### EFFECT_USER6
*(OS 7.0+)* 

### EFFECT_USER7
*(OS 7.0+)* 

### EFFECT_USER8
*(OS 7.0+)* 


## Errors
### EFFECT_SD_CARD_NOT_FOUND
*(OS 7.0+)* 

### EFFECT_ERROR_IN_FONT_DIRECTORY
*(OS 7.0+)* 

### EFFECT_ERROR_IN_BLADE_ARRAY
*(OS 7.0+)* 

### EFFECT_FONT_DIRECTORY_NOT_FOUND
*(OS 7.0+)* 

