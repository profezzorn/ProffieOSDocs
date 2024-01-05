---
title: Functions Template Syntax Summary
---

Here’s a summary list of all of the "Usage: " comment sections from the header files for  
functions as of ProffieOS 7.13.  

For example, if you were looking for what arguments Bump<> takes,  
now you’d know that it takes Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>.  

## [AltF, SyncAltToVarianceF, SyncAltToVarianceL](https://github.com/profezzorn/ProffieOS/blob/master/functions/alt.h)  
Usage: AltF  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;Returns current_alternative for use in ColorSelect<>, TrSelect<> or IntSelect<>  
Usage: SyncAltToVarianceF  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER (always zero)  
&nbsp;&nbsp;&nbsp;&nbsp;Enables Bidirectional synchronization between ALT and VARIANCE.  
&nbsp;&nbsp;&nbsp;&nbsp;If variance changes, so does alt, if alt changes, so does variance.  
Usage: SyncAltToVarianceL  
&nbsp;&nbsp;&nbsp;&nbsp;return value: LAYER (transparent)  
&nbsp;&nbsp;&nbsp;&nbsp;Synchronizes alt to variance, just put it somewhere in the layer stack. (but not first)  

## [BatteryLevel](https://github.com/profezzorn/ProffieOS/blob/master/functions/battery_level.h)  
Usage: BatteryLevel  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on battery level.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  

## [BladeAngleX](https://github.com/profezzorn/ProffieOS/blob/master/functions/blade_angle.h)  
Usage: BladeAngleX<MIN, MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on angle of blade  
&nbsp;&nbsp;&nbsp;&nbsp;MIN : FUNCTION (defaults to Int<0>)  
&nbsp;&nbsp;&nbsp;&nbsp;MAX : FUNCTION (defaults to Int<32768>)  
&nbsp;&nbsp;&nbsp;&nbsp;MIN and MAX specifies the range of angles which are used.  
&nbsp;&nbsp;&nbsp;&nbsp;For MIN and MAX 0 means down and 32768 means up and 16384 means  
&nbsp;&nbsp;&nbsp;&nbsp;pointing towards the horizon.  
&nbsp;&nbsp;&nbsp;&nbsp;So if MIN=16484 and MAX=32768, BladeAngle will return zero when you  
&nbsp;&nbsp;&nbsp;&nbsp;point the blade towards the horizon and 32768 when you point it  
&nbsp;&nbsp;&nbsp;&nbsp;straight up. Any angle below the horizon will also return zero.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: FUNCTION, same for all LEDs.  

## [BlastF, BlastFadeoutF, OriginalBlastF](https://github.com/profezzorn/ProffieOS/blob/master/functions/blast.h)  
Usage: BlastF<FADEOUT_MS, WAVE_SIZE, WAVE_MS, EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;FADOUT_MS: a number (defaults to 200)  
&nbsp;&nbsp;&nbsp;&nbsp;WAVE_SIZE: a number (defaults to 100)  
&nbsp;&nbsp;&nbsp;&nbsp;WAVE_MS: a number (defaults to 400)  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;This function is intended to be used in a Mix<> or AlphaL<>  
&nbsp;&nbsp;&nbsp;&nbsp;When a blast occurs, it makes a wave starting at the blast  
&nbsp;&nbsp;&nbsp;&nbsp;location (which is currently random) and travels out  
&nbsp;&nbsp;&nbsp;&nbsp;from that direction. At the peak, this function returns  
&nbsp;&nbsp;&nbsp;&nbsp;32768 and when there is no blast it returns zero.  
&nbsp;&nbsp;&nbsp;&nbsp;The FADOUT_MS controls how long it takes the wave to  
&nbsp;&nbsp;&nbsp;&nbsp;fade out. The WAVE_SIZE controls the width of the wave.  
&nbsp;&nbsp;&nbsp;&nbsp;The WAVE_MS parameter controls the speed of the waves.  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT can be used to trigger this effect by something  
&nbsp;&nbsp;&nbsp;&nbsp;other than a blast effect.  
Usage: BlastFadeoutF<FADEOUT_MS, EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;FADEOUT_MS: a number (defaults to 250)  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;NOrmally returns 0, but returns up to 32768 when the  
&nbsp;&nbsp;&nbsp;&nbsp;selected effect occurs. Then if fades back to zero over  
&nbsp;&nbsp;&nbsp;&nbsp;FADEOUT_MS milliseconds.  
Usage: OriginalBlastF<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Original blast function. Normally returns zero, but  
&nbsp;&nbsp;&nbsp;&nbsp;returns up to 32768 when the selected effect occurs.  

## [BlinkingF](https://github.com/profezzorn/ProffieOS/blob/master/functions/blinking.h)  
Usage: BlinkingF<A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>  
&nbsp;&nbsp;&nbsp;&nbsp;BLINK_MILLIS: a number  
&nbsp;&nbsp;&nbsp;&nbsp;BLINK_PROMILLE: a number, defaults to 500  
&nbsp;&nbsp;&nbsp;&nbsp;BLINK_MILLIS_FUNC: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;BLINK_PROMILLE_FUNC: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Switches between 0 and 32768  
&nbsp;&nbsp;&nbsp;&nbsp;A full cycle from 0 to 328768 and back again takes BLINK_MILLIS milliseconds.  
&nbsp;&nbsp;&nbsp;&nbsp;If BLINK_PROMILLE is 500, we select A for the first half and B for the  
&nbsp;&nbsp;&nbsp;&nbsp;second half. If BLINK_PROMILLE is smaller, we get less A and more B.  
&nbsp;&nbsp;&nbsp;&nbsp;If BLINK_PROMILLE is 0, we get all 0.  
&nbsp;&nbsp;&nbsp;&nbsp;If BLINK_PROMILLE is 1000 we get all 32768.  

## [BrownNoiseF, SlowNoise](https://github.com/profezzorn/ProffieOS/blob/master/functions/brown_noise.h)  
Usage: BrownNoiseF<GRADE>  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns a value between 0 and 32768 with nearby pixels being similar.  
&nbsp;&nbsp;&nbsp;&nbsp;GRADE controls how similar nearby pixels are.  
Usage: SlowNoise<SPEED>  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns a value between 0 and 32768 which changes randomly up and  
&nbsp;&nbsp;&nbsp;&nbsp;down over time. All pixels gets the same value.  
&nbsp;&nbsp;&nbsp;&nbsp;SPEED controls how quickly the value changes.  

## [Bump, HumpFlickerFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/bump.h)  
Usage: Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns different values for each LED, forming a bump shape.  
&nbsp;&nbsp;&nbsp;&nbsp;If BUMP_POSITION is 0, bump will be at the hilt.  
&nbsp;&nbsp;&nbsp;&nbsp;If BUMP_POSITION is 32768, the bump will be at the tip.  
&nbsp;&nbsp;&nbsp;&nbsp;If BUMP_WIDTH_FRACTION is 1, bump will be extremely narrow.  
&nbsp;&nbsp;&nbsp;&nbsp;If BUMP_WIDTH_FRACTION is 32768, it will fill up most/all of the blade.  
&nbsp;&nbsp;&nbsp;&nbsp;BUMP_POSITION, BUMP_WIDTH_FRACTION: INTEGER  
Usage: HumpFlickerFX<FUNCTION>  
&nbsp;&nbsp;&nbsp;&nbsp;or: HumpFlickerF<N>  
&nbsp;&nbsp;&nbsp;&nbsp;FUNCTION: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;N: NUMBER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;Creates hump shapes that randomize over the blade.  
&nbsp;&nbsp;&nbsp;&nbsp;The returned INTEGER is the size of the humps.  
&nbsp;&nbsp;&nbsp;&nbsp;Large values can give the blade a shimmering look,   
&nbsp;&nbsp;&nbsp;&nbsp;while small values look more like speckles.  

## [CenterDistF](https://github.com/profezzorn/ProffieOS/blob/master/functions/center_dist.h)  
Usage: Remap<CenterDistF< CENTER>,COLOR>  
&nbsp;&nbsp;&nbsp;&nbsp;Distributes led COLOR from CENTER  
&nbsp;&nbsp;&nbsp;&nbsp;CENTER : FUNCTION (defaults to Int<16384>)  

## [ChangeSlowly](https://github.com/profezzorn/ProffieOS/blob/master/functions/change_slowly.h)  
Usage: ChangeSlowly<F, SPEED>  
&nbsp;&nbsp;&nbsp;&nbsp;Changes F by no more than SPEED values per second.  
&nbsp;&nbsp;&nbsp;&nbsp;F, SPEED: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION, same for all LEDs  

## [CircularSectionF](https://github.com/profezzorn/ProffieOS/blob/master/functions/circular_section.h)  
Usage: CircularSectionF<POSITION, FRACTION>  
&nbsp;&nbsp;&nbsp;&nbsp;POSITION: FUNCTION position on the circle or blade, 0-32768  
&nbsp;&nbsp;&nbsp;&nbsp;FRACTION: FUNCTION how much of the blade to light up, 0 = none, 32768 = all of it  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 32768 for LEDs near the position with wrap-around.  
&nbsp;&nbsp;&nbsp;&nbsp;Could be used with MarbleF<> for a marble effect, or with  
&nbsp;&nbsp;&nbsp;&nbsp;Saw<> for a spinning/colorcycle type effect.  
&nbsp;&nbsp;&nbsp;&nbsp;Example: If POSITION = 0 and FRACTION = 16384, then this function  
&nbsp;&nbsp;&nbsp;&nbsp;will return 32768 for the first 25% and the last 25% of the blade  
&nbsp;&nbsp;&nbsp;&nbsp;and 0 for the rest of the LEDs.  

## [ClampF, ClampFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/clamp.h)  
Usage: ClampF<F, MIN, MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;Or: ClampFX<F, MINCLASS, MAXCLASS>  
&nbsp;&nbsp;&nbsp;&nbsp;Clamps value between MIN and MAX  
&nbsp;&nbsp;&nbsp;&nbsp;F, MIN, MAX: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;MINCLASS, MAXCLASS: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [ClashImpactFX](https://github.com/profezzorn/ProffieOS/blob/master/functions/clash_impact.h)  
Usage: ClashImpactFX<MIN, MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;MIN is minimum value Clash is detected (recommended range 0 ~ 500, default is 200)  
&nbsp;&nbsp;&nbsp;&nbsp;MAX is maximum impact to return 32768 (recommended range 1000 ~ 1600, default is 1600)  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on impact strength of clash  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  

## [Divide](https://github.com/profezzorn/ProffieOS/blob/master/functions/divide.h)  
Usage: Divide<F, V>  
&nbsp;&nbsp;&nbsp;&nbsp;Divide F by V  
&nbsp;&nbsp;&nbsp;&nbsp;If V = 0, returns 0  
&nbsp;&nbsp;&nbsp;&nbsp;F, V: FUNCTION,   
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Please note that Divide<> isn't an exact inverse of Mult<> because mult uses fixed-point mathematics  
&nbsp;&nbsp;&nbsp;&nbsp;(it divides the result by 32768) while Divide<> doesn't, it just returns F / V  

## [EffectPulse, LockupPulseF, IncrementWithReset, EffectIncrementF](https://github.com/profezzorn/ProffieOS/blob/master/functions/effect_increment.h)  
Usage: EffectPulse<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: BladeEffectType  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 32768 once for each time the given effect occurs.  
Usage: LockupPulseF<LOCKUP_TYPE>  
&nbsp;&nbsp;&nbsp;&nbsp;LOCKUP_TYPE: a SaberBase::LockupType  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 32768 once for each time the given lockup occurs.  
Usage: IncrementWithReset<PULSE, RESET_PULSE, MAX, I>  
&nbsp;&nbsp;&nbsp;&nbsp;PULSE: FUNCTION (pulse type)   
&nbsp;&nbsp;&nbsp;&nbsp;RESET_PULSEE: FUNCTION (pulse type) defaults to Int<0> (no reset)  
&nbsp;&nbsp;&nbsp;&nbsp;MAX, I: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Starts at zero, increments by I each time the PULSE occurse.  
&nbsp;&nbsp;&nbsp;&nbsp;If it reaches MAX it stays there.  
&nbsp;&nbsp;&nbsp;&nbsp;Resets back to zero when RESET_PULSE occurs.  
Usage: EffectIncrementF<EFFECT, MAX, I>  
&nbsp;&nbsp;&nbsp;&nbsp;Increases by value I (up to MAX) each time EFFECT is triggered  
&nbsp;&nbsp;&nbsp;&nbsp;If current value + I = MAX, it returns 0.  
&nbsp;&nbsp;&nbsp;&nbsp;If adding I exceeds MAX, the function returns 0 + any remainder in excesss of MAX   
&nbsp;&nbsp;&nbsp;&nbsp;I, MAX = numbers  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [EffectPosition](https://github.com/profezzorn/ProffieOS/blob/master/functions/effect_position.h)  
Usage: EffectPosition<>  
&nbsp;&nbsp;&nbsp;&nbsp;Or: EffectPosition<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: effect type  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;EffectPosition returns the position of a particular effect. 0 = base, 32768 = tip.  
&nbsp;&nbsp;&nbsp;&nbsp;For now, this location is random, but may be set explicitly in the future.  
&nbsp;&nbsp;&nbsp;&nbsp;When used as EffectPosition<> inside a TransitionEffectL whose EFFECT is already specified,   
&nbsp;&nbsp;&nbsp;&nbsp;then it will automatically use the right effect.  

## [HoldPeakF](https://github.com/profezzorn/ProffieOS/blob/master/functions/hold_peak.h)  
Usage: HoldPeakF<F, HOLD_MILLIS, SPEED>  
&nbsp;&nbsp;&nbsp;&nbsp;Holds Peak value of F for HOLD_MILLIS.  
&nbsp;&nbsp;&nbsp;&nbsp;then transitions down over SPEED to current F  
&nbsp;&nbsp;&nbsp;&nbsp;F, HOLD_MILLIS and SPEED: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION, same for all LEDs  

## [Ifon, InOutFunc](https://github.com/profezzorn/ProffieOS/blob/master/functions/ifon.h)  
Usage: Ifon<A, B>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns A if saber is on, B otherwise.  
&nbsp;&nbsp;&nbsp;&nbsp;A, B: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
Usage: InOutFunc<OUT_MILLIS, IN_MILLIS>  
&nbsp;&nbsp;&nbsp;&nbsp;IN_MILLIS, OUT_MILLIS: a number  
&nbsp;&nbsp;&nbsp;&nbsp;RETURN VALUE: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;0 when off, 32768 when on, takes OUT_MILLIS to go from 0 to 32768  
&nbsp;&nbsp;&nbsp;&nbsp;takes IN_MILLIS to go from 32768 to 0.  

## [IncrementModulo, ThresholdPulseF, IncrementF](https://github.com/profezzorn/ProffieOS/blob/master/functions/increment.h)  
Usage: IncrementModulo<PULSE, MAX, INCREMENT>  
&nbsp;&nbsp;&nbsp;&nbsp;PULSE: FUNCTION (pulse type)  
&nbsp;&nbsp;&nbsp;&nbsp;MAX: FUNCTION (not zero) defaults to Int<32768>  
&nbsp;&nbsp;&nbsp;&nbsp;INCREMENT: FUNCTION defaults to Int<1>  
&nbsp;&nbsp;&nbsp;&nbsp;Increments by I each time PULSE occurs wraps around when  
&nbsp;&nbsp;&nbsp;&nbsp;it reaches MAX.  
Usage: ThresholdPulseF<F, THRESHOLD, HYST_PERCENT>  
&nbsp;&nbsp;&nbsp;&nbsp;F: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;THRESHOLD: FUNCTION (defaults to Int<32768>)  
&nbsp;&nbsp;&nbsp;&nbsp;HYST_PERCENT: FUNCTION (defaults to Int<66>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 32768 once when F > THRESHOLD, then waits until  
&nbsp;&nbsp;&nbsp;&nbsp;F < THRESHOLD * HYST_PERCENT / 100 before going back  
&nbsp;&nbsp;&nbsp;&nbsp;to the initial state (waiting for F > THRESHOLD).  
Usage: IncrementF<F, V, MAX, I, HYST_PERCENT>  
&nbsp;&nbsp;&nbsp;&nbsp;Increases by value I (up to MAX) each time F >= V  
&nbsp;&nbsp;&nbsp;&nbsp;Detection resets once F drops below V * HYST_PERCENT  
&nbsp;&nbsp;&nbsp;&nbsp;if greater than MAX returns 0  
&nbsp;&nbsp;&nbsp;&nbsp;F, V, I, MAX = numbers  
&nbsp;&nbsp;&nbsp;&nbsp;HYST_PERCENT = percent (defaults to 66)  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [Int](https://github.com/profezzorn/ProffieOS/blob/master/functions/int.h)  
Usage: Int<N>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns N  
&nbsp;&nbsp;&nbsp;&nbsp;N: a number  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [IntSelect](https://github.com/profezzorn/ProffieOS/blob/master/functions/int_select.h)  
Usage: IntSelect<SELECTION, Int1, Int2...>  
&nbsp;&nbsp;&nbsp;&nbsp;SELECTION: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns SELECTION of N   
&nbsp;&nbsp;&nbsp;&nbsp;If SELECTION is 0, the first integer is returned, if SELECTION is 1, the second and so forth.  
&nbsp;&nbsp;&nbsp;&nbsp;N: numbers  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [IsBetween](https://github.com/profezzorn/ProffieOS/blob/master/functions/isbetween.h)  
Usage: IsBetween<F, BOTTOM, TOP>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0 or 32768 based F > BOTTOM and < TOP   
&nbsp;&nbsp;&nbsp;&nbsp;F, BOTTOM, TOP: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [IsLessThan](https://github.com/profezzorn/ProffieOS/blob/master/functions/islessthan.h)  
Usage: IsLessThan<F, V>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0 or 32768 based on V  
&nbsp;&nbsp;&nbsp;&nbsp;If F < V returns 32768, if F >= V returns 0   
&nbsp;&nbsp;&nbsp;&nbsp;F, V: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [LayerFunctions](https://github.com/profezzorn/ProffieOS/blob/master/functions/layer_functions.h)  
Usage: LayerFunctions<F1, F2, ...>  
&nbsp;&nbsp;&nbsp;&nbsp;F1, F2: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns (32768 - (32768 - F1) * (32768 * F2) / 32768)  
&nbsp;&nbsp;&nbsp;&nbsp;This is the same as 1-(1-F1)*(1-F2), but multiplied by 32768.  
&nbsp;&nbsp;&nbsp;&nbsp;Basically Mix<LayerFunctions<F1, F2>, A, B> is the same as Mix<F2, Mix<F1, A, B>, B>.  

## [LinearSectionF](https://github.com/profezzorn/ProffieOS/blob/master/functions/linear_section.h)  
Usage: LinearSectionF<POSITION, FRACTION>  
&nbsp;&nbsp;&nbsp;&nbsp;POSITION: FUNCTION position on the blade, 0-32768  
&nbsp;&nbsp;&nbsp;&nbsp;FRACTION: FUNCTION how much of the blade to light up, 0 = none  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;creates a "block" of pixels at POSITION taking up FRACTION of blade  

## [MarbleF](https://github.com/profezzorn/ProffieOS/blob/master/functions/marble.h)  
Usage: MarbleF<OFFSET, FRICTION, ACCELERATION, GRAVITY>  
&nbsp;&nbsp;&nbsp;&nbsp;OFFSET: FUNCTION  0-32768, adjust until "down" represents is actually down  
&nbsp;&nbsp;&nbsp;&nbsp;FRICTION: FUNCTION, higher values makes the marble slow down, usually a constant  
&nbsp;&nbsp;&nbsp;&nbsp;ACCELERATION: FUNCTION, a function specifying how much speed to add to the marble  
&nbsp;&nbsp;&nbsp;&nbsp;GRAVITY: FUNCTION higher values makes the marble heavier  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  0-32768, representing point on a circle  
&nbsp;&nbsp;&nbsp;&nbsp;This is intended for a small ring of neopixels.  
&nbsp;&nbsp;&nbsp;&nbsp;It runs a simulation of a marble trapped in a circular  
&nbsp;&nbsp;&nbsp;&nbsp;track and returns the position of that marble.  
&nbsp;&nbsp;&nbsp;&nbsp;Meant to be used with CircularSectionF to turn the marble  
&nbsp;&nbsp;&nbsp;&nbsp;position into a lighted up section.  

## [ModF](https://github.com/profezzorn/ProffieOS/blob/master/functions/mod.h)  
Usage: ModF<F, MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;F: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;MAX: FUNCTION (not zero)  
&nbsp;&nbsp;&nbsp;&nbsp;When F is greater than MAX, F wraps to 0  
&nbsp;&nbsp;&nbsp;&nbsp;When F is less than 0, F wraps to MAX  
&nbsp;&nbsp;&nbsp;&nbsp;returns Integer  

## [Mult, Percentage](https://github.com/profezzorn/ProffieOS/blob/master/functions/mult.h)  
Usage: Mult<F, V>  
&nbsp;&nbsp;&nbsp;&nbsp;Fixed point multiplication of values F * V,   
&nbsp;&nbsp;&nbsp;&nbsp;fixed point 16.15 arithmetic (32768 = 1.0)  
&nbsp;&nbsp;&nbsp;&nbsp;(2*2 would not result in 4),   
&nbsp;&nbsp;&nbsp;&nbsp;(16384 * 16384 = 8192, representation of 0.5*0.5=0.25)   
&nbsp;&nbsp;&nbsp;&nbsp;most blade functions use this method of fixed point calculations  
&nbsp;&nbsp;&nbsp;&nbsp;F, V: INTEGER,   
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
Usage: Percentage<F, V>  
&nbsp;&nbsp;&nbsp;&nbsp;Gets Percentage V of value F,   
&nbsp;&nbsp;&nbsp;&nbsp;Percentages over 100% are allowed and will effectively be a multiplier.   
&nbsp;&nbsp;&nbsp;&nbsp;F, V: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;example Percentage<Int<16384>,25>  
&nbsp;&nbsp;&nbsp;&nbsp;this will give you 25% of Int<16384> and returns Int<4096>  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [OnsparkF](https://github.com/profezzorn/ProffieOS/blob/master/functions/on_spark.h)  
Usage: OnsparkF<MILLIS>  
&nbsp;&nbsp;&nbsp;&nbsp;MILLIS: FUNCTION (defaults to Int<200>)  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;When the blade turns on, this function starts returning  
&nbsp;&nbsp;&nbsp;&nbsp;32768, then fades back to zero over MILLIS milliseconds.  
&nbsp;&nbsp;&nbsp;&nbsp;This is intended to be used with Mix<> or AlphaL<> to  
&nbsp;&nbsp;&nbsp;&nbsp;to create a flash of color or white when the blade ignites.  

## [RampF](https://github.com/profezzorn/ProffieOS/blob/master/functions/ramp.h)  
Usage: RampF  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0 at base and 32768 at tip.  
&nbsp;&nbsp;&nbsp;&nbsp;Example: Mix<RampF, COLOR1, COLOR2, COLOR3>  
&nbsp;&nbsp;&nbsp;&nbsp;This would do the same thing as Gradient<COLOR1, COLOR2, COLOR3>  

## [RandomF, RandomPerLEDF, EffectRandomF](https://github.com/profezzorn/ProffieOS/blob/master/functions/random.h)  
Usage: RandomF  
&nbsp;&nbsp;&nbsp;&nbsp;Return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns a random number between 0 and 32768.  
&nbsp;&nbsp;&nbsp;&nbsp;All LEDS gets the same value.  
Usage: RandomPerLEDF  
&nbsp;&nbsp;&nbsp;&nbsp;Return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Returns a random number between 0 and 32768.  
&nbsp;&nbsp;&nbsp;&nbsp;Each LED gets a different random value.  
Usage: EffectRandomF<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns a random value between 0 and 32768 each time EVENT is triggered  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [RandomBlinkF](https://github.com/profezzorn/ProffieOS/blob/master/functions/random_blink.h)  
Usage: RandomBlinkF<MILLIHZ>  
&nbsp;&nbsp;&nbsp;&nbsp;MILLHZ: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Randomly returns either 0 or 32768 for each LED. The returned value  
&nbsp;&nbsp;&nbsp;&nbsp;is held, but changed to a new random value MILLIHZ * 1000 times per  
&nbsp;&nbsp;&nbsp;&nbsp;second.  

## [ReadPinF, AnalogReadPinF](https://github.com/profezzorn/ProffieOS/blob/master/functions/readpin.h)  
Usage: ReadPinF<PIN>  
&nbsp;&nbsp;&nbsp;&nbsp;or: ReadPinF<PIN, PIN_MODE>  
&nbsp;&nbsp;&nbsp;&nbsp;returns INTEGER, 0 if pin is low and 32768 if pin is high  
&nbsp;&nbsp;&nbsp;&nbsp;PIN: int, pin you want your style to respond to  
&nbsp;&nbsp;&nbsp;&nbsp;PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT  
Usage: AnalogReadPinF<PIN>  
&nbsp;&nbsp;&nbsp;&nbsp;or: AnalogReadPinF<PIN, PIN_MODE>  
&nbsp;&nbsp;&nbsp;&nbsp;returns INTEGER, 0-32768 depending on input reading.  
&nbsp;&nbsp;&nbsp;&nbsp;PIN: int, pin you want your style to respond to  
&nbsp;&nbsp;&nbsp;&nbsp;PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT  
&nbsp;&nbsp;&nbsp;&nbsp;Notes:  
&nbsp;&nbsp;&nbsp;&nbsp;  * May cause slowdowns  
&nbsp;&nbsp;&nbsp;&nbsp;  * may not update every run() call  
&nbsp;&nbsp;&nbsp;&nbsp;  * pin modes other than INPUT may not be supported,  
&nbsp;&nbsp;&nbsp;&nbsp;  * Only analog-capable pins will work.  

## [Scale](https://github.com/profezzorn/ProffieOS/blob/master/functions/scale.h)  
Usage: Scale<F, A, B>  
&nbsp;&nbsp;&nbsp;&nbsp;Changes values in range 0 - 32768 to A-B  
&nbsp;&nbsp;&nbsp;&nbsp;F, A, B: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [SequenceF](https://github.com/profezzorn/ProffieOS/blob/master/functions/sequence.h)  
usage: SequenceF<millis_per_bits, bits, 0b0000000000000000, ....>  
&nbsp;&nbsp;&nbsp;&nbsp;millis_per_bit: a number, millseconds spent on each bit  
&nbsp;&nbsp;&nbsp;&nbsp;bits: a number, number of bits before we loop around to the beginning  
&nbsp;&nbsp;&nbsp;&nbsp;0b0000000000000000: 16-bit binary numbers containing the actual sequence.  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 32768 if the current bit in the sequence is 1, 0 otherwise.  
&nbsp;&nbsp;&nbsp;&nbsp;The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.  
&nbsp;&nbsp;&nbsp;&nbsp;Note that if not all bits are used within the 16-bit number.  
&nbsp;&nbsp;&nbsp;&nbsp;Example, an SOS pattern:  
&nbsp;&nbsp;&nbsp;&nbsp;SequenceF<100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>  

## [Sin](https://github.com/profezzorn/ProffieOS/blob/master/functions/sin.h)  
Usage: Sin<RPM, LOW, HIGH>  
&nbsp;&nbsp;&nbsp;&nbsp;pulses between LOW - HIGH RPM times per minute  
&nbsp;&nbsp;&nbsp;&nbsp;LOW: INTEGER (defaults to Int<0>)  
&nbsp;&nbsp;&nbsp;&nbsp;HIGH: INTEGER (defaults to Int<32768>)  
&nbsp;&nbsp;&nbsp;&nbsp;RPM: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [SliceF](https://github.com/profezzorn/ProffieOS/blob/master/functions/slice.h)  
Usage: SliceF<DENSITY_FUNCTION>  
&nbsp;&nbsp;&nbsp;&nbsp;or: SliceF<DENSITY_FUNCTION, OFFSET>  
&nbsp;&nbsp;&nbsp;&nbsp;DENSITY_FUNCTION: 3DF   
&nbsp;&nbsp;&nbsp;&nbsp;OFFSET: integer, defaults to 20  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;The DENSITY_FUNCTION is a 3-dimensional function, f(x, y, z)  
&nbsp;&nbsp;&nbsp;&nbsp;the SliceF function calculates the x/y/z coordinates based on the  
&nbsp;&nbsp;&nbsp;&nbsp;angle of the blade. For now, the only density functions available  
&nbsp;&nbsp;&nbsp;&nbsp;are SmokeDF and FastSmokeDF, which are basically the same thing.  
&nbsp;&nbsp;&nbsp;&nbsp;This is very similar to how the POV blade works, but instead of  
&nbsp;&nbsp;&nbsp;&nbsp;using a large data blob as input, it just uses another function  
&nbsp;&nbsp;&nbsp;&nbsp;as input.  

## [SmoothStep](https://github.com/profezzorn/ProffieOS/blob/master/functions/smoothstep.h)  
Usage: SmoothStep<POS, WIDTH>  
&nbsp;&nbsp;&nbsp;&nbsp;POS, WIDTH: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;POS: specifies the middle of the smoothstep, 0 = base of blade, 32768=tip  
&nbsp;&nbsp;&nbsp;&nbsp;WIDTH: witdth of transition, 0 = no transition, 32768 = length of blade  
&nbsp;&nbsp;&nbsp;&nbsp;Example: SmoothStep<Int<16384>, Int<16384>> returns 0 up until 25% of the blade.  
&nbsp;&nbsp;&nbsp;&nbsp;From there it has a smooth transition to 32768, which will be reached at 75% of  
&nbsp;&nbsp;&nbsp;&nbsp;the blade. If WIDTH is negative, the transition will go the other way.  

## [SmoothSoundLevel, NoisySoundLevel, NoisySoundLevelCompat](https://github.com/profezzorn/ProffieOS/blob/master/functions/sound_level.h)  
Usage: SmoothSoundLevel  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on sound level.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  
Usage: NoisySoundLevel  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on sound level.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  
Usage: NoisySoundLevelCompat  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on sound level.  
&nbsp;&nbsp;&nbsp;&nbsp;This function is now used to implement the  
&nbsp;&nbsp;&nbsp;&nbsp;AudioFlicker<> style, don't change it.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  

## [SparkleF](https://github.com/profezzorn/ProffieOS/blob/master/functions/sparkle.h)  
Usage: SparkleF<SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>  
&nbsp;&nbsp;&nbsp;&nbsp;SPARK_CHANCE_PROMILLE: a number  
&nbsp;&nbsp;&nbsp;&nbsp;SPARK_INTENSITY: a number  

## [StrobeF](https://github.com/profezzorn/ProffieOS/blob/master/functions/strobe.h)  
Usage: StrobeF<STROBE_FREQUENCY, STROBE_MILLIS>  
&nbsp;&nbsp;&nbsp;&nbsp;STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS  
&nbsp;&nbsp;&nbsp;&nbsp;STROBE_FREQUENCY times per second.  

## [Subtract](https://github.com/profezzorn/ProffieOS/blob/master/functions/subtract.h)  
Usage: Subtract<A, B>  
&nbsp;&nbsp;&nbsp;&nbsp;Subtracts B from A (A - B)  
&nbsp;&nbsp;&nbsp;&nbsp;A, B: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;return value: FUNCTION  

## [SUM](https://github.com/profezzorn/ProffieOS/blob/master/functions/sum.h)  
Usage: SUM<A, B, ...>  
&nbsp;&nbsp;&nbsp;&nbsp;Adds A + B...  
&nbsp;&nbsp;&nbsp;&nbsp;A, B: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [SwingSpeed](https://github.com/profezzorn/ProffieOS/blob/master/functions/swing_speed.h)  
Usage: SwingSpeed<MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on swing speed  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  
Usage: SwingAcceleration<MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on swing acceleration  
&nbsp;&nbsp;&nbsp;&nbsp;MAX defaults to 150  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  

## [TimeSinceEffect](https://github.com/profezzorn/ProffieOS/blob/master/functions/time_since_effect.h)  
Usage: TimeSinceEffect<>  
&nbsp;&nbsp;&nbsp;&nbsp;Or: TimeSinceEffect<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: effect type  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;TimeSinceEffect returns the number of milliseconds since a particular  
&nbsp;&nbsp;&nbsp;&nbsp;effect occured.  
&nbsp;&nbsp;&nbsp;&nbsp;When used as TimeSinceEffect<> inside a TransitionEffectL whose EFFECT is already specified,   
&nbsp;&nbsp;&nbsp;&nbsp;then it will automatically use the right effect.  

## [Trigger](https://github.com/profezzorn/ProffieOS/blob/master/functions/trigger.h)  
Usage: Trigger<EFFECT, FADE_IN_MILLIS, SUSTAIN_MILLIS, FADE_OUT_MILLIS, DELAY>  
&nbsp;&nbsp;&nbsp;&nbsp;Normally returns 0, but when EFFECT occurs, it ramps up to 32768,  
&nbsp;&nbsp;&nbsp;&nbsp;stays there for SUSTAIN_MILLIS, then fades down to zero again.  
&nbsp;&nbsp;&nbsp;&nbsp;If delay is specified, the whole thing is delayed that much before it starts.  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: BladeEffectType  
&nbsp;&nbsp;&nbsp;&nbsp;FADE_IN_MILLIS: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;SUSTAIN_MILLIS: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;FADE_OUT_MILLIS: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;DELAY_MILLIS: INTEGER (defaults to Int<0>)  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  

## [TwistAngle, TwistAcceleration](https://github.com/profezzorn/ProffieOS/blob/master/functions/twist_angle.h)  
Usage: TwistAngle<N, OFFSET>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on angle of twist  
&nbsp;&nbsp;&nbsp;&nbsp;OFFSET: Adjustable offset (0-32768) to make the twistangle values line up with how you hold the hilt.  
&nbsp;&nbsp;&nbsp;&nbsp;N : Number of times the values goes from 0 to 32768 and back per hilt revolution.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: FUNCTION, same for all leds  
Usage: TwistAcceleration<MAX>  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on acceleration of twist in one direction  
&nbsp;&nbsp;&nbsp;&nbsp;MAX : Maximum acceleration needed to return 32768  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: FUNCTION, same for all leds  

## [Variation](https://github.com/profezzorn/ProffieOS/blob/master/functions/variation.h)  
Usage: Variation  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on current variation.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: FUNCTION  
&nbsp;&nbsp;&nbsp;&nbsp;Note that using Variation in your style means that the  
&nbsp;&nbsp;&nbsp;&nbsp;the automatic color rotation is turned off. The color wheel  
&nbsp;&nbsp;&nbsp;&nbsp;menu is unaffected, but the style is now responsible for actually  
&nbsp;&nbsp;&nbsp;&nbsp;changing the color.  
&nbsp;&nbsp;&nbsp;&nbsp;Note that if any blade styles are using ColorChange<>,  
&nbsp;&nbsp;&nbsp;&nbsp;the variation will return "ticked" values: 0, 1, 2, etc.  

## [VolumeLevel](https://github.com/profezzorn/ProffieOS/blob/master/functions/volume_level.h)  
Usage: VolumeLevel  
&nbsp;&nbsp;&nbsp;&nbsp;Returns 0-32768 based on volume level.  
&nbsp;&nbsp;&nbsp;&nbsp;returned value: INTEGER  

## [WavLen](https://github.com/profezzorn/ProffieOS/blob/master/functions/wavlen.h)  
Usage: WavLen<>  
&nbsp;&nbsp;&nbsp;&nbsp;Or: WavLen<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: effect type  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;WavLen (length of wav file) takes the duration of a wav file sound  
&nbsp;&nbsp;&nbsp;&nbsp;and can be used to replace time integer arguments in a blade style.  
&nbsp;&nbsp;&nbsp;&nbsp;Example: TrFadeX<WavLen<EFFECT_RETRACTION>>  
&nbsp;&nbsp;&nbsp;&nbsp;When used as WavLen<> inside a TransitionEffectL whose EFFECT is already specified,   
&nbsp;&nbsp;&nbsp;&nbsp;then it will automatically use the right effect.  
&nbsp;&nbsp;&nbsp;&nbsp;Example: TransitionEffectL<TrConcat<TrWipex<WavLen<>>,White,TrWipeX<WavLen<>>>,EFFECT_BLAST>  

## [WavNum](https://github.com/profezzorn/ProffieOS/blob/master/functions/wavnum.h)  
Usage: WavNum<>  
&nbsp;&nbsp;&nbsp;&nbsp;Or: WavNum<EFFECT>  
&nbsp;&nbsp;&nbsp;&nbsp;EFFECT: effect type  
&nbsp;&nbsp;&nbsp;&nbsp;return value: INTEGER  
&nbsp;&nbsp;&nbsp;&nbsp;Returns which file was actually played.  
&nbsp;&nbsp;&nbsp;&nbsp;First file returns 0. Even if the file is called 'clash1.wav'.  
  
