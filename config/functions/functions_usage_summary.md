---
title: Functions Template Syntax Summary
---

Here’s a summary list of all of the "Usage: " comment sections from the header files for  
functions as of ProffieOS 7.13.  

For example, if you were looking for what arguments Bump<> takes,  
now you’d know that it takes Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>.  

## [AltF, SyncAltToVarianceF, SyncAltToVarianceL](https://github.com/profezzorn/ProffieOS/blob/master/functions/alt.h)  
Usage: AltF  
return value: INTEGER  
Returns current_alternative for use in ColorSelect<>, TrSelect<> or IntSelect<>  

Usage: SyncAltToVarianceF  
return value: INTEGER (always zero)  
Enables Bidirectional synchronization between ALT and VARIANCE.  
If variance changes, so does alt, if alt changes, so does variance.  

Usage: SyncAltToVarianceL  
return value: LAYER (transparent)  
Synchronizes alt to variance, just put it somewhere in the layer stack. (but not first)  

## [BatteryLevel](https://github.com/profezzorn/ProffieOS/blob/master/functions/battery_level.h)  
Usage: BatteryLevel  
Returns 0-32768 based on battery level.  
returned value: INTEGER  

## [BladeAngleX](https://github.com/profezzorn/ProffieOS/blob/master/functions/blade_angle.h)  
Usage: BladeAngleX<MIN, MAX>  
Returns 0-32768 based on angle of blade  
MIN : FUNCTION (defaults to Int<0>)  
MAX : FUNCTION (defaults to Int<32768>)  
MIN and MAX specifies the range of angles which are used.  
For MIN and MAX 0 means down and 32768 means up and 16384 means  
pointing towards the horizon.  
So if MIN=16484 and MAX=32768, BladeAngle will return zero when you  
point the blade towards the horizon and 32768 when you point it  
straight up. Any angle below the horizon will also return zero.  
returned value: FUNCTION, same for all LEDs.  

## [BlastF, BlastFadeoutF, OriginalBlastF](https://github.com/profezzorn/ProffieOS/blob/master/functions/blast.h)  
Usage: BlastF<FADEOUT_MS, WAVE_SIZE, WAVE_MS, EFFECT>  
FADOUT_MS: a number (defaults to 200)  
WAVE_SIZE: a number (defaults to 100)  
WAVE_MS: a number (defaults to 400)  
EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
returned value: FUNCTION  
This function is intended to be used in a Mix<> or AlphaL<>  
When a blast occurs, it makes a wave starting at the blast  
location (which is currently random) and travels out  
from that direction. At the peak, this function returns  
32768 and when there is no blast it returns zero.  
The FADOUT_MS controls how long it takes the wave to  
fade out. The WAVE_SIZE controls the width of the wave.  
The WAVE_MS parameter controls the speed of the waves.  
EFFECT can be used to trigger this effect by something  
other than a blast effect.  

Usage: BlastFadeoutF<FADEOUT_MS, EFFECT>  
FADEOUT_MS: a number (defaults to 250)  
EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
return value: FUNCTION  
NOrmally returns 0, but returns up to 32768 when the  
selected effect occurs. Then if fades back to zero over  
FADEOUT_MS milliseconds.  

Usage: OriginalBlastF<EFFECT>  
EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
return value: FUNCTION  
Original blast function. Normally returns zero, but  
returns up to 32768 when the selected effect occurs.  

## [BlinkingF](https://github.com/profezzorn/ProffieOS/blob/master/functions/blinking.h)  
Usage: BlinkingF<A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>  
BLINK_MILLIS: a number  
BLINK_PROMILLE: a number, defaults to 500  
BLINK_MILLIS_FUNC: FUNCTION  
BLINK_PROMILLE_FUNC: FUNCTION  
return value: FUNCTION  
Switches between 0 and 32768  
A full cycle from 0 to 328768 and back again takes BLINK_MILLIS milliseconds.  
If BLINK_PROMILLE is 500, we select A for the first half and B for the  
second half. If BLINK_PROMILLE is smaller, we get less A and more B.  
If BLINK_PROMILLE is 0, we get all 0.  
If BLINK_PROMILLE is 1000 we get all 32768.  


## [BrownNoiseF, SlowNoise](https://github.com/profezzorn/ProffieOS/blob/master/functions/brown_noise.h)  
Usage: BrownNoiseF<GRADE>  
return value: FUNCTION  
Returns a value between 0 and 32768 with nearby pixels being similar.  
GRADE controls how similar nearby pixels are.  

Usage: SlowNoise<SPEED>  
return value: FUNCTION  
Returns a value between 0 and 32768 which changes randomly up and  
down over time. All pixels gets the same value.  
SPEED controls how quickly the value changes.  

## [Bump, HumpFlickerFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/bump.h)  
Usage: Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>  
Returns different values for each LED, forming a bump shape.  
If BUMP_POSITION is 0, bump will be at the hilt.  
If BUMP_POSITION is 32768, the bump will be at the tip.  
If BUMP_WIDTH_FRACTION is 1, bump will be extremely narrow.  
If BUMP_WIDTH_FRACTION is 32768, it will fill up most/all of the blade.  
BUMP_POSITION, BUMP_WIDTH_FRACTION: INTEGER  

Usage: HumpFlickerFX<FUNCTION>  
or: HumpFlickerF<N>  
FUNCTION: FUNCTION  
N: NUMBER  
return value: INTEGER  
Creates hump shapes that randomize over the blade.  
The returned INTEGER is the size of the humps.  
Large values can give the blade a shimmering look,   
while small values look more like speckles.  

## [CenterDistF](https://github.com/profezzorn/ProffieOS/blob/master/functions/center_dist.h)  
Usage: Remap<CenterDistF\<CENTER>,COLOR>  
Distributes led COLOR from CENTER  
CENTER : FUNCTION (defaults to Int<16384>)  

## [ChangeSlowly](https://github.com/profezzorn/ProffieOS/blob/master/functions/change_slowly.h)  
Usage: ChangeSlowly<F, SPEED>  
Changes F by no more than SPEED values per second.  
F, SPEED: FUNCTION  
return value: FUNCTION, same for all LEDs  

## [CircularSectionF](https://github.com/profezzorn/ProffieOS/blob/master/functions/circular_section.h)  
Usage: CircularSectionF<POSITION, FRACTION>  
POSITION: FUNCTION position on the circle or blade, 0-32768  
FRACTION: FUNCTION how much of the blade to light up, 0 = none, 32768 = all of it  
return value: FUNCTION  
Returns 32768 for LEDs near the position with wrap-around.  
Could be used with MarbleF<> for a marble effect, or with  
Saw<> for a spinning/colorcycle type effect.  
Example: If POSITION = 0 and FRACTION = 16384, then this function  
will return 32768 for the first 25% and the last 25% of the blade  
and 0 for the rest of the LEDs.  

## [ClampF, ClampFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/clamp.h)  
Usage: ClampF<F, MIN, MAX>  
Or: ClampFX<F, MINCLASS, MAXCLASS>  
Clamps value between MIN and MAX  
F, MIN, MAX: INTEGER  
MINCLASS, MAXCLASS: FUNCTION  
return value: INTEGER  

## [ClashImpactFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/clash_impact.h)  
Usage: ClashImpactFX<MIN, MAX>  
MIN is minimum value Clash is detected (recommended range 0 ~ 500, default is 200)  
MAX is maximum impact to return 32768 (recommended range 1000 ~ 1600, default is 1600)  
Returns 0-32768 based on impact strength of clash  
returned value: INTEGER  

## [Divide](https://github.com/profezzorn/ProffieOS/blob/master/functions/divide.h)  
Usage: Divide<F, V>  
Divide F by V  
If V = 0, returns 0  
F, V: FUNCTION,   
return value: FUNCTION  
Please note that Divide<> isn't an exact inverse of Mult<> because mult uses fixed-point mathematics  
(it divides the result by 32768) while Divide<> doesn't, it just returns F / V  

## [EffectPulse, LockupPulseF, IncrementWithReset, EffectIncrementF](https://github.com/profezzorn/ProffieOS/blob/master/functions/effect_increment.h)  
Usage: EffectPulse<EFFECT>  
EFFECT: BladeEffectType  
Returns 32768 once for each time the given effect occurs.  

Usage: LockupPulseF<LOCKUP_TYPE>  
LOCKUP_TYPE: a SaberBase::LockupType  
Returns 32768 once for each time the given lockup occurs.  

Usage: IncrementWithReset<PULSE, RESET_PULSE, MAX, I>  
PULSE: FUNCTION (pulse type)   
RESET_PULSEE: FUNCTION (pulse type) defaults to Int<0> (no reset)  
MAX, I: FUNCTION  
Starts at zero, increments by I each time the PULSE occurse.  
If it reaches MAX it stays there.  
Resets back to zero when RESET_PULSE occurs.  

Usage: EffectIncrementF<EFFECT, MAX, I>  
Increases by value I (up to MAX) each time EFFECT is triggered  
If current value + I = MAX, it returns 0.  
If adding I exceeds MAX, the function returns 0 + any remainder in excesss of MAX   
I, MAX = numbers  
return value: INTEGER  

## [EffectPosition](https://github.com/profezzorn/ProffieOS/blob/master/functions/effect_position.h)  
Usage: EffectPosition<>  
Or: EffectPosition<EFFECT>  
EFFECT: effect type  
return value: INTEGER  
EffectPosition returns the position of a particular effect. 0 = base, 32768 = tip.  
For now, this location is random, but may be set explicitly in the future.  
When used as EffectPosition<> inside a TransitionEffectL whose EFFECT is already specified,   
then it will automatically use the right effect.  

## [HoldPeakF](https://github.com/profezzorn/ProffieOS/blob/master/functions/hold_peak.h)  
Usage: HoldPeakF<F, HOLD_MILLIS, SPEED>  
Holds Peak value of F for HOLD_MILLIS.  
then transitions down over SPEED to current F  
F, HOLD_MILLIS and SPEED: FUNCTION  
return value: FUNCTION, same for all LEDs  

## [Ifon, InOutFunc](https://github.com/profezzorn/ProffieOS/blob/master/functions/ifon.h)  
Usage: Ifon<A, B>  
Returns A if saber is on, B otherwise.  
A, B: INTEGER  
return value: INTEGER  

Usage: InOutFunc<OUT_MILLIS, IN_MILLIS>  
IN_MILLIS, OUT_MILLIS: a number  
RETURN VALUE: FUNCTION  
0 when off, 32768 when on, takes OUT_MILLIS to go from 0 to 32768  
takes IN_MILLIS to go from 32768 to 0.  

## [IncrementModulo, ThresholdPulseF, IncrementF](https://github.com/profezzorn/ProffieOS/blob/master/functions/increment.h)  
Usage: IncrementModulo<PULSE, MAX, INCREMENT>  
PULSE: FUNCTION (pulse type)  
MAX: FUNCTION (not zero) defaults to Int<32768>  
INCREMENT: FUNCTION defaults to Int<1>  
Increments by I each time PULSE occurs wraps around when  
it reaches MAX.  

Usage: ThresholdPulseF<F, THRESHOLD, HYST_PERCENT>  
F: FUNCTION  
THRESHOLD: FUNCTION (defaults to Int<32768>)  
HYST_PERCENT: FUNCTION (defaults to Int<66>  
Returns 32768 once when F > THRESHOLD, then waits until  
F < THRESHOLD * HYST_PERCENT / 100 before going back  
to the initial state (waiting for F > THRESHOLD).  

Usage: IncrementF<F, V, MAX, I, HYST_PERCENT>  
Increases by value I (up to MAX) each time F >= V  
Detection resets once F drops below V * HYST_PERCENT  
if greater than MAX returns 0  
F, V, I, MAX = numbers  
HYST_PERCENT = percent (defaults to 66)  
return value: INTEGER  

## [Int](https://github.com/profezzorn/ProffieOS/blob/master/functions/int.h)  
Usage: Int<N>  
Returns N  
N: a number  
return value: INTEGER  

## [IntSelect](https://github.com/profezzorn/ProffieOS/blob/master/functions/int_select.h)  
Usage: IntSelect<SELECTION, Int1, Int2...>  
SELECTION: FUNCTION  
Returns SELECTION of N   
If SELECTION is 0, the first integer is returned, if SELECTION is 1, the second and so forth.  
N: numbers  
return value: INTEGER  

## [IsBetween](https://github.com/profezzorn/ProffieOS/blob/master/functions/isbetween.h)  
Usage: IsBetween<F, BOTTOM, TOP>  
Returns 0 or 32768 based F > BOTTOM and < TOP   
F, BOTTOM, TOP: INTEGER  
return value: INTEGER  

## [IsLessThan](https://github.com/profezzorn/ProffieOS/blob/master/functions/islessthan.h)  
Usage: IsLessThan<F, V>  
Returns 0 or 32768 based on V  
If F < V returns 32768, if F >= V returns 0   
F, V: INTEGER  
return value: INTEGER  

## [LayerFunctions](https://github.com/profezzorn/ProffieOS/blob/master/functions/layer_functions.h)  
Usage: LayerFunctions<F1, F2, ...>  
F1, F2: FUNCTION  
return value: FUNCTION  
Returns (32768 - (32768 - F1) * (32768 * F2) / 32768)  
This is the same as 1-(1-F1)*(1-F2), but multiplied by 32768.  
Basically Mix<LayerFunctions<F1, F2>, A, B> is the same as Mix<F2, Mix<F1, A, B>, B>.  

## [LinearSectionF](https://github.com/profezzorn/ProffieOS/blob/master/functions/linear_section.h)  
Usage: LinearSectionF<POSITION, FRACTION>  
POSITION: FUNCTION position on the blade, 0-32768  
FRACTION: FUNCTION how much of the blade to light up, 0 = none  
return value: FUNCTION  
creates a "block" of pixels at POSITION taking up FRACTION of blade  

## [MarbleF](https://github.com/profezzorn/ProffieOS/blob/master/functions/marble.h)  
Usage: MarbleF<OFFSET, FRICTION, ACCELERATION, GRAVITY>  
OFFSET: FUNCTION  0-32768, adjust until "down" represents is actually down  
FRICTION: FUNCTION, higher values makes the marble slow down, usually a constant  
ACCELERATION: FUNCTION, a function specifying how much speed to add to the marble  
GRAVITY: FUNCTION higher values makes the marble heavier  
return value: FUNCTION  0-32768, representing point on a circle  
This is intended for a small ring of neopixels.  
It runs a simulation of a marble trapped in a circular  
track and returns the position of that marble.  
Meant to be used with CircularSectionF to turn the marble  
position into a lighted up section.  

## [ModF](https://github.com/profezzorn/ProffieOS/blob/master/functions/mod.h)  
Usage: ModF<F, MAX>  
F: FUNCTION  
MAX: FUNCTION (not zero)  
When F is greater than MAX, F wraps to 0  
When F is less than 0, F wraps to MAX  
returns Integer  

## [Mult](https://github.com/profezzorn/ProffieOS/blob/master/functions/mult.h)  
Usage: Mult<F, V>  
Fixed point multiplication of values F * V,   
fixed point 16.15 arithmetic (32768 = 1.0)  
(2*2 would not result in 4),   
(16384 * 16384 = 8192, representation of 0.5*0.5=0.25)   
most blade functions use this method of fixed point calculations  
F, V: INTEGER,   
return value: INTEGER  

## [Percentage](https://github.com/profezzorn/ProffieOS/blob/master/functions/mult.h)  
Usage: Percentage<F, V>  
Gets Percentage V of value F,   
Percentages over 100% are allowed and will effectively be a multiplier.   
F, V: INTEGER  
example Percentage<Int<16384>,25>  
this will give you 25% of Int<16384> and returns Int<4096>  
return value: INTEGER  

Usage: Percentage<F, V>  
Gets Percentage V of value F,   
Percentages over 100% are allowed and will effectively be a multiplier.   
F, V: INTEGER  
example Percentage<Int<16384>,25>  
this will give you 25% of Int<16384> and returns Int<4096>  
return value: INTEGER  

## [OnsparkF](https://github.com/profezzorn/ProffieOS/blob/master/functions/on_spark.h)  
Usage: OnsparkF<MILLIS>  
MILLIS: FUNCTION (defaults to Int<200>)  
return value: FUNCTION  
When the blade turns on, this function starts returning  
32768, then fades back to zero over MILLIS milliseconds.  
This is intended to be used with Mix<> or AlphaL<> to  
to create a flash of color or white when the blade ignites.  

## [RampF](https://github.com/profezzorn/ProffieOS/blob/master/functions/ramp.h)  
Usage: RampF  
Returns 0 at base and 32768 at tip.  
Example: Mix<RampF, COLOR1, COLOR2, COLOR3>  
This would do the same thing as Gradient<COLOR1, COLOR2, COLOR3>  

## [RandomF, RandomPerLEDF, EffectRandomF](https://github.com/profezzorn/ProffieOS/blob/master/functions/random.h)  
Usage: RandomF  
Return value: FUNCTION  
Returns a random number between 0 and 32768.  
All LEDS gets the same value.  

Usage: RandomPerLEDF  
Return value: FUNCTION  
Returns a random number between 0 and 32768.  
Each LED gets a different random value.  

Usage: EffectRandomF<EFFECT>  
Returns a random value between 0 and 32768 each time EVENT is triggered  
return value: INTEGER  

## [RandomBlinkF](https://github.com/profezzorn/ProffieOS/blob/master/functions/random_blink.h)  
Usage: RandomBlinkF<MILLIHZ>  
MILLHZ: FUNCTION  
Randomly returns either 0 or 32768 for each LED. The returned value  
is held, but changed to a new random value MILLIHZ * 1000 times per  
second.  

## [Scale](https://github.com/profezzorn/ProffieOS/blob/master/functions/scale.h)  
Usage: Scale<F, A, B>  
Changes values in range 0 - 32768 to A-B  
F, A, B: INTEGER  
return value: INTEGER  

## [SequenceF](https://github.com/profezzorn/ProffieOS/blob/master/functions/sequence.h)  
usage: SequenceF<millis_per_bits, bits, 0b0000000000000000, ....>  
millis_per_bit: a number, millseconds spent on each bit  
bits: a number, number of bits before we loop around to the beginning  
0b0000000000000000: 16-bit binary numbers containing the actual sequence.  
Returns 32768 if the current bit in the sequence is 1, 0 otherwise.  
The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.  
Note that if not all bits are used within the 16-bit number.  
Example, an SOS pattern:  
SequenceF<100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>  

## [Sin](https://github.com/profezzorn/ProffieOS/blob/master/functions/sin.h)  
Usage: Sin<RPM, LOW, HIGH>  
pulses between LOW - HIGH RPM times per minute  
LOW: INTEGER (defaults to Int<0>)  
HIGH: INTEGER (defaults to Int<32768>)  
RPM: INTEGER  
return value: INTEGER  

## [SliceF](https://github.com/profezzorn/ProffieOS/blob/master/functions/slice.h)  
Usage: SliceF<DENSITY_FUNCTION>  
or: SliceF<DENSITY_FUNCTION, OFFSET>  
DENSITY_FUNCTION: 3DF   
OFFSET: integer, defaults to 20  
return value: FUNCTION  
The DENSITY_FUNCTION is a 3-dimensional function, f(x, y, z)  
the SliceF function calculates the x/y/z coordinates based on the  
angle of the blade. For now, the only density functions available  
are SmokeDF and FastSmokeDF, which are basically the same thing.  
This is very similar to how the POV blade works, but instead of  
using a large data blob as input, it just uses another function  
as input.  

## [SmoothStep](https://github.com/profezzorn/ProffieOS/blob/master/functions/smoothstep.h)  
Usage: SmoothStep<POS, WIDTH>  
POS, WIDTH: FUNCTION  
return value: FUNCTION  
POS: specifies the middle of the smoothstep, 0 = base of blade, 32768=tip  
WIDTH: witdth of transition, 0 = no transition, 32768 = length of blade  
Example: SmoothStep<Int<16384>, Int<16384>> returns 0 up until 25% of the blade.  
From there it has a smooth transition to 32768, which will be reached at 75% of  
the blade. If WIDTH is negative, the transition will go the other way.  

## [SmoothSoundLevel, NoisySoundLevel, NoisySoundLevelCompat](https://github.com/profezzorn/ProffieOS/blob/master/functions/sound_level.h)  
Usage: SmoothSoundLevel  
Returns 0-32768 based on sound level.  
returned value: INTEGER  

Usage: NoisySoundLevel  
Returns 0-32768 based on sound level.  
returned value: INTEGER  

Usage: NoisySoundLevelCompat  
Returns 0-32768 based on sound level.  
This function is now used to implement the  
AudioFlicker<> style, don't change it.  
returned value: INTEGER  

## [SparkleF](https://github.com/profezzorn/ProffieOS/blob/master/functions/sparkle.h)  
Usage: SparkleF<SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>  
SPARK_CHANCE_PROMILLE: a number  
SPARK_INTENSITY: a number  

## [StrobeF](https://github.com/profezzorn/ProffieOS/blob/master/functions/strobe.h)  
Usage: StrobeF<STROBE_FREQUENCY, STROBE_MILLIS>  
STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION  
return value: INTEGER  
Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS  
STROBE_FREQUENCY times per second.  

## [Subtract](https://github.com/profezzorn/ProffieOS/blob/master/functions/subtract.h)  
Usage: Subtract<A, B>  
Subtracts B from A (A - B)  
A, B: FUNCTION  
return value: FUNCTION  

## [SUM](https://github.com/profezzorn/ProffieOS/blob/master/functions/sum.h)  
Usage: SUM<A, B, ...>  
Adds A + B...  
A, B: INTEGER  
return value: INTEGER  

## [SwingSpeed](https://github.com/profezzorn/ProffieOS/blob/master/functions/swing_speed.h)  
Usage: SwingSpeed<MAX>  
Returns 0-32768 based on swing speed  
returned value: INTEGER  

Usage: SwingAcceleration<MAX>  
Returns 0-32768 based on swing acceleration  
MAX defaults to 150  
returned value: INTEGER  

## [TimeSinceEffect](https://github.com/profezzorn/ProffieOS/blob/master/functions/time_since_effect.h)  
Usage: TimeSinceEffect<>  
Or: TimeSinceEffect<EFFECT>  
EFFECT: effect type  
return value: INTEGER  
TimeSinceEffect returns the number of milliseconds since a particular  
effect occured.  
When used as TimeSinceEffect<> inside a TransitionEffectL whose EFFECT is already specified,   
then it will automatically use the right effect.  

## [Trigger](https://github.com/profezzorn/ProffieOS/blob/master/functions/trigger.h)  
Usage: Trigger<EFFECT, FADE_IN_MILLIS, SUSTAIN_MILLIS, FADE_OUT_MILLIS, DELAY>  
Normally returns 0, but when EFFECT occurs, it ramps up to 32768,  
stays there for SUSTAIN_MILLIS, then fades down to zero again.  
If delay is specified, the whole thing is delayed that much before it starts.  
EFFECT: BladeEffectType  
FADE_IN_MILLIS: INTEGER  
SUSTAIN_MILLIS: INTEGER  
FADE_OUT_MILLIS: INTEGER  
DELAY_MILLIS: INTEGER (defaults to Int<0>)  
return value: INTEGER  

## [TwistAngle, TwistAcceleration](https://github.com/profezzorn/ProffieOS/blob/master/functions/twist_angle.h)  
Usage: TwistAngle<N, OFFSET>  
Returns 0-32768 based on angle of twist  
OFFSET: Adjustable offset (0-32768) to make the twistangle values line up with how you hold the hilt.  
N : Number of times the values goes from 0 to 32768 and back per hilt revolution.  
returned value: FUNCTION, same for all leds  

Usage: TwistAcceleration<MAX>  
Returns 0-32768 based on acceleration of twist in one direction  
MAX : Maximum acceleration needed to return 32768  
returned value: FUNCTION, same for all leds  

## [Variation](https://github.com/profezzorn/ProffieOS/blob/master/functions/variation.h)  
Usage: Variation  
Returns 0-32768 based on current variation.  
returned value: FUNCTION  
Note that using Variation in your style means that the  
the automatic color rotation is turned off. The color wheel  
menu is unaffected, but the style is now responsible for actually  
changing the color.  
Note that if any blade styles are using ColorChange<>,  
the variation will return "ticked" values: 0, 1, 2, etc.  

## [VolumeLevel](https://github.com/profezzorn/ProffieOS/blob/master/functions/volume_level.h)  
Usage: VolumeLevel  
Returns 0-32768 based on volume level.  
returned value: INTEGER  

## [WavLen](https://github.com/profezzorn/ProffieOS/blob/master/functions/wavlen.h)  
Usage: WavLen<>  
Or: WavLen<EFFECT>  
EFFECT: effect type  
return value: INTEGER  
WavLen (length of wav file) takes the duration of a wav file sound  
and can be used to replace time integer arguments in a blade style.  
Example: TrFadeX<WavLen<EFFECT_RETRACTION>>  
When used as WavLen<> inside a TransitionEffectL whose EFFECT is already specified,   
then it will automatically use the right effect.  
Example: TransitionEffectL<TrConcat<TrWipex<WavLen<>>,White,TrWipeX<WavLen<>>>,EFFECT_BLAST>  

## [WavNum](https://github.com/profezzorn/ProffieOS/blob/master/functions/wavnum.h)  
Usage: WavNum<>  
Or: WavNum<EFFECT>  
EFFECT: effect type  
return value: INTEGER  
Returns which file was actually played.  
First file returns 0. Even if the file is called 'clash1.wav'.  

