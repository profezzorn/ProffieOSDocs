---
title: Transitions Template Syntax Summary
---

Here’s a summary list of all of the "Usage: " comment sections from the header files for  
transitions as of ProffieOS 7.13.  

For example, if you were looking for what arguments TrDoEffectX<> takes,  
now you’d know that it takes TrDoEffectX<TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS>.  


## [TrBlinkX, TrBlink](https://github.com/profezzorn/ProffieOS/blob/master/transitions/blink.h)  
Usage: TrBlinkX<MILLIS_FUNCTION, N, WIDTH_FUNCTION>  
or: TrBlink<MILLIS, N, WIDTH>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
N: a number  
WIDTH_FUNCTION: FUNCTION, defaults to Int<16384>  
WIDTH: a number, defaults to 16384  
return value: TRANSITION  
Blinks A-B N times in MILLIS, based on WIDTH (0 ~ 32768)  
If WIDTH = 16384 A and B appear equally, lower decreases length of A, higher increases length of A  

## [TrFadeX, TrFade](https://github.com/profezzorn/ProffieOS/blob/master/transitions/boing.h)  
Usage: TrFadeX<MILLIS_FUNCTION, N>  
or: TrFade<MILLIS, N>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
N: a number  
return value: TRANSITION  
Similar to TrFade, but transitions back and forth between the two  
colors several times. (As specified by N). If N is 0, it's equal to  
TrFade. If N is 1 it transitions A-B-A-B, if N is 2, it is A-B-A-B-A-B,  
and so on.  

## [TrCenterWipeX, TrCenterWipe](https://github.com/profezzorn/ProffieOS/blob/master/transitions/center_wipe.h)  
Usage: TrCenterWipeX<POSITION_FUNCTION, MILLIS_FUNCTION>  
or: TrCenterWipe<POSITION, MILLIS>  
POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION  
POSITION: Int  
MILLIS: a number  
return value: TRANSITION  
In the beginning entire blade is color A, then color B   
starts at the POSTION and extends up and down the blade  
in the specified number of milliseconds.  

Usage: TrCenterWipeInX<POSITION_FUNCTION, MILLIS_FUNCTION>  
or: TrCenterWipeIn<POSITION, MILLIS>  
POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION  
POSITION: Int  
MILLIS: a number  
return value: TRANSITION  
In the beginning entire blade is color A, then color B   
starts at the ends and moves toward POSITION  
in the specified number of milliseconds.  

## [TrColorCycleX, TrColorCycle](https://github.com/profezzorn/ProffieOS/blob/master/transitions/colorcycle.h)  
Usage: TrColorCycle<MILLIS, START_RPM, END_RPM>  
OR: Usage: TrColorCycleX<MILLIS_FUNCTION, START_RPM, END_RPM>  
MILLS:  number  
MILLIS_FUNCTION: FUNCTION  
START_RPM: a number (defaults to 0)  
END_RPM: a number (defaults to 6000)  
return value: COLOR  
Tron-like transition.  

## [TrConcat](https://github.com/profezzorn/ProffieOS/blob/master/transitions/concat.h)  
Usage: TrConcat<TRANSITION, INTERMEDIATE, TRANSITION, ...>  
OR:  TrConcat<TRANSITION, TRANSITION, ...>  
TRANSITION: TRANSITION  
INTERMEDIATE: COLOR  
return value: TRANSITION  
Concatenates any number of transitions.  
If an intermediate color is provided, we first transition to that color, then  
we transition away from it in the next transition.  
If no intermediate color is provided, the first and second transition will both  
transition from the same input colors. If for instance both the first and second  
transitions are TrFades, then there will be a jump in the middle as the transition  
will go back and start from the beginning. Using TimeReverseX on the second transition  
will avoid this, as the second transition will then run backwards.  

## [TrDelayX, TrDelay](https://github.com/profezzorn/ProffieOS/blob/master/transitions/delay.h)  
Usage: TrDelayX<MILLIS_FUNCTION>  
or: TrDelay<MILLIS>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
return value: TRANSITION  
Waits for the specified number of milliseconds, then transitions  
to second color. Menant to be used with TrConcat  

## [TrDoEffectX, TrDoEffect](https://github.com/profezzorn/ProffieOS/blob/master/transitions/doeffect.h)  
Usage: TrDoEffectX<TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS>  
or: TrDoEffect<TRANSITION, EFFECT, WAVNUM, LOCATION>  
TRANSITION: TRANSITION  
EFFECT: effect type  
WAVNUM, LOCATION: a number  
LOCATION_CLASS: INTEGER  
return value: TRANSITION  
Runs the specified TRANSITION and triggers EFFECT (unless the blade is off)  
Can specify WAV file to use for EFFECT with WAVNUM  
NOTE: 0 is first wav file, -1 is random wav  
LOCATION = -1 is random  

Usage: TrDoEffectAlwaysX<TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS>  
or: TrDoEffectsAlways<TRANSITION, EFFECT, WAVNUM, LOCATION>  
TrDoEffectAlways is the same as TrDoEffectX, but runs even if  
the blade is off.  

## [TrExtendX, TrExtend](https://github.com/profezzorn/ProffieOS/blob/master/transitions/extend.h)  
Usage: TrExtendX<MILLIS_FUNCTION, TRANSITION>  
or: TrExtend<MILLIS, TRANSITION>  
MILLIS_FUNCTION: FUNCTION  
TRANSITION: TRANSITION  
MILLIS: a number  
return value: TRANSITION  
Runs the specified transition, then holds the  
last value for some additional time specified by  
MILLIS_FUNCTION.  

## [TrFadeX, TrFade](https://github.com/profezzorn/ProffieOS/blob/master/transitions/fade.h)  
Usage: TrFadeX<MILLIS_FUNCTION>  
or: TrFade<MILLIS>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
return value: TRANSITION  
Linear fading between two colors in specified number of milliseconds.  

Usage: TrSmoothFadeX<MILLIS_FUNCTION>  
or: TrSmoothFade<MILLIS>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
return value: TRANSITION  
Similar to TrFade, but uses a cubic fading function  
so fading starts slow, speeds up in the middle, then  
slows down at the end.  

## [TrInstant](https://github.com/profezzorn/ProffieOS/blob/master/transitions/instant.h)  
Usage: TrInstant  
return value: TRANSITION  
Instant transition.  

## [TrJoin, TrJoinR](https://github.com/profezzorn/ProffieOS/blob/master/transitions/join.h)  
Usage: TrJoin<TR1, TR2, ...>  
TR1, TR2: TRANSITION  
return value: TRANSITION  
A little hard to explain, but all the specified  
transitions are run in parallel. Basically, we  
chain transitions like ((A TR1 B) TR2 B)  

Usage: TrJoinR<TR1, TR2, ...>  
TR1, TR2: TRANSITION  
return value: TRANSITION  
Similar to TrJoin, but transitions are chained  
to the right instead of to the left. Like:  
(A TR2 (A TR1 B))  

## [TrLoop, TrLoopNX, TrLoopUntil](https://github.com/profezzorn/ProffieOS/blob/master/transitions/loop.h)  
Usage: TrLoop<TRANSITION>  
TRANSITION: TRANSITION  
Return Value: TRANSITION  
Runs the specified transition in a loop forever.  

Usage: TrLoopNX<N_FUNCTION, TRANSITION>  
or: TrLoopN<N, TRANSITION>  
N_FUNCTION: FUNCTION (number of Loops)  
N: a number (Loops)  
TRANSITION: TRANSITION  
Return Value: TRANSITION  
Runs the specified transition N times.  

Usage: TrLoopUntil<PULSE, TRANSITION, OUT>  
TRANSITION, OUT: TRANSITION  
PULSE: FUNCTION (pulse)  
Return Value: TRANSITION  
Runs the specified transition until the pulse occurs.  
When the pulse occurs, the loop continues, but OUT is used to  
transition away from it, and when OUT is done, the transition is done.  

## [TrRandom](https://github.com/profezzorn/ProffieOS/blob/master/transitions/random.h)  
Usage: TrRandom<TR1, TR2, ...>  
TR1, TR2: TRANSITION  
return value: TRANSITION  
Each time a new transition is started, a random  
transition is picked from the specified list of  
transitions.  

## [TrSelect](https://github.com/profezzorn/ProffieOS/blob/master/transitions/select.h)  
Usage: TrSelect<SELECTION, TR1, TR2, ...>  
SELECTION: FUNCTION  
TR1, TR2: TRANSITION  
return value: TRANSITION  
transition option is picked from the specified list of  
transitions based on Int<>  
with Int<0> representing first transition  

## [TrSequence](https://github.com/profezzorn/ProffieOS/blob/master/transitions/sequence.h)  
Usage: TrSequence<TR1, TR2, ...>  
TR1, TR2: TRANSITION  
return value: TRANSITION  
transition options used in sequence  

## [TrWaveX, TrSparkX](https://github.com/profezzorn/ProffieOS/blob/master/transitions/wave.h)  
Usage: TrWaveX<COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER>  
COLOR: COLOR  
FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER: FUNCTIONS  
TrWave is implements a wave traveling out from a specified point.  
It's based on the Blast effect and is meant to look like a ripple starting  
at a point on the blade. Unlike other transitions, this effect starts and ends  
at the same color, and the wave is drawn using COLOR instead of the start/end  
colors like most transitions do. It's intended to be used with TransitionLoopL  
or TransitionEffectL, which take transitions that start and begin with the same  
color.  

Usage: TrSparkX< COLOR, SPARK_SIZE, SPARK_MS, SPARK_CENTER>  
COLOR: COLOR  
SPARK_SIZE, SPARK_MS, SPARK_CENTER: FUNCTIONS  
TrSparkX generates a wave without Fade over the length of the blade from   
SPARK_CENTER. Unlike other transitions, this effect starts and ends  
at the same color, and the wave is drawn using COLOR instead of the start/end  
colors like most transitions do. It's intended to be used with TransitionLoopL  
or TransitionEffectL, which take transitions that start and begin with the same  
color.  

## [TrWipe, TrWipeIn, TrWipeSparkTip, TrWipeInSparkTip, and X variants](https://github.com/profezzorn/ProffieOS/blob/master/transitions/wipe.h)  
Usage: TrWipeX<MILLIS_FUNCTION>  
or: TrWipe<MILLIS>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
return value: TRANSITION  
Similar to saber ignition. In the beginning  
entire blade is color A, then color B starts at the base  
and extends up to the tip of the blade in the specified  
number of milliseconds.  

Usage: TrWipeInX<MILLIS_FUNCTION>  
or: TrWipeIn<MILLIS>  
MILLIS_FUNCTION: FUNCTION  
MILLIS: a number  
return value: TRANSITION  
Like TrWipe, but from tip to base.  

Usage: TrWipeSparkTip<SPARK_COLOR, MILLIS, SIZE>  
SPARK_COLOR = COLOR  
MILLIS = a number  
SIZE = a number  
return value: TRANSITION  
Same as TrWipe, but adds a "spark" tip to the  
leading edge of the wipe color.  

Usage: TrWipeInSparkTip<SPARK_COLOR, MILLIS, SIZE>  
SPARK_COLOR = COLOR  
MILLIS = a number  
SIZE = a number  
return value: TRANSITION  
Like TrWipeSparkTip, but from tip to base.  

