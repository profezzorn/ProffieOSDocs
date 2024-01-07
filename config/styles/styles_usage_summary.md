---
title: Styles Template Syntax Summary
---

Here’s a summary list of all of the "Usage: " comment sections from the header files for  
styles as of ProffieOS 7.13.  

For example, if you were looking for what arguments BlastL<> takes,  
now you’d know that it takes BlastL<BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>.  

## [AlphaL](https://github.com/profezzorn/ProffieOS/blob/master/styles/alpha.h)  
Usage: AlphaL<COLOR, ALPHA>  
COLOR: COLOR or LAYER  
ALPHA: FUNCTION  
Return value: LAYER  
This function makes a color transparent. The ALPHA function specifies just how opaque it should be.  
If ALPHA is zero, the returned color will be 100% transparent. If Alpha is 32768, the returned color will  
be 100% opaque. Note that if COLOR is already transparent, it will be made more transparent. Example:  
If COLOR is 50% opaque, and ALPHA returns 16384, the result will be 25% opaque.  

## [AudioFlicker, AudioFlickerL](https://github.com/profezzorn/ProffieOS/blob/master/styles/audio_flicker.h)  
Usage: AudioFlicker<A, B>  
OR: AudioFlickerL\<B>  
A, B: COLOR  
return value: COLOR  
Mixes between A and B based on audio. Quiet audio  
means more A, loud audio means more B.  
Based on a single sample instead of an average to make it flicker.  

## [Blast, BlastL](https://github.com/profezzorn/ProffieOS/blob/master/styles/blast.h)  
Usage: Blast<BASE, BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>  
OR: BlastL<BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>  
BASE, BLAST: COLOR  
FADEOUT_MS: a number (defaults to 150)  
WAVE_SIZE: a number (defaults to 100)  
WAVE_MS: a number (defaults to 400)  
return value: COLOR  
Normally shows BASE, but creates a blast effect using  
the color BLAST when a blast is requested. The effect  
is basically two humps moving out from the blast location.  
The size of the humps can be changed with WAVE_SIZE, note  
that smaller values makes the humps bigger. WAVE_MS determines  
how fast the waves travel. Smaller values makes the waves  
travel slower. Finally FADEOUT_MS determines how fast the  
humps fade back to the base color.  

Usage: OriginalBlast<BASE, BLAST>  
OR: OriginalBlastL<BLAST>  
BASE, BLAST: COLOR  
return value: COLOR  
Normally shows BASE, but creates a blast effect using  
the color BLAST when a blast is requested.  
This was the original blast effect, but it is slow and not  
very configurable.  

## [Blinking, BlinkingX, BlinkingL](https://github.com/profezzorn/ProffieOS/blob/master/styles/blinking.h)  
Usage: Blinking<A, B, BLINK_MILLIS, BLINK_PROMILLE>  
OR: BlinkingX<A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>  
OR: BlinkingL<B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>  
A, B: COLOR  
BLINK_MILLIS: a number  
BLINK_PROMILLE: a number, defaults to 500  
BLINK_MILLIS_FUNC: FUNCTION  
BLINK_PROMILLE_FUNC: FUNCTION  
return value: COLOR  
Switches between A and B.  
A full cycle from A to B and back again takes BLINK_MILLIS milliseconds.  
If BLINK_PROMILLE is 500, we select A for the first half and B for the  
second half. If BLINK_PROMILLE is smaller, we get less A and more B.  
If BLINK_PROMILLE is 0, we get all B.  
If BLINK_PROMILLE is 1000 we get all A.  

## [BrownNoiseFlicker, BrownNoiseFlickerL](https://github.com/profezzorn/ProffieOS/blob/master/styles/brown_noise_flicker.h)  
Usage: BrownNoiseFlicker<A, B, grade>  
OR: BrownNoiseFlickerL<B, grade>  
A, B: COLOR  
grade: int  
return value: COLOR  
Randomly selects between A and B, but keeps nearby  
pixels looking similar.  

## [ByteOrderStyle](https://github.com/profezzorn/ProffieOS/blob/master/styles/byteorder.h)  
Usage: ByteOrderStyle<BYTEORDER, COLOR>  
BYTEORDER: Color8::RGB, or one of the other byte orders  
COLOR: COLOR  
return value: COLOR  

## [&style_charging](https://github.com/profezzorn/ProffieOS/blob/master/styles/charging.h)  
Usage: &style_charging  
return value: POINTER  
Charging blade style.  
Slowly pulsating battery indicator.  

## [SimpleClash, SimpleClashL, LocalizedClash, LocalizedClashL](https://github.com/profezzorn/ProffieOS/blob/master/styles/clash.h)  
Usage: SimpleClash<BASE, CLASH_COLOR, CLASH_MILLIS>  
OR: SimpleClashL<CLASH_COLOR, CLASH_MILLIS>  
BASE: COLOR  
CLASH_COLOR: COLOR (defaults to white)  
CLASH_MILLIS: a number (defaults to 40)  
return value: COLOR  
Turns the blade to CLASH_COLOR for CLASH_MILLIS millseconds  
when a clash occurs.  

Usage: LocalizedClash<BASE, CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>  
Usage: LocalizedClashL<CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>  
BASE: COLOR  
CLASH_COLOR: COLOR (defaults to white)  
CLASH_MILLIS: a number (defaults to 40)  
return value: COLOR  
Similar to SimpleClash, but lights up a portion of the blade.  
The fraction of the blade is defined by CLASH_WIDTH_PERCENT  
The location of the clash is random within the middle half of the blade.  
Localized clashes should work well with stabs with no modifications.  

## [ColorCycle](https://github.com/profezzorn/ProffieOS/blob/master/styles/color_cycle.h)  
Usage: ColorCycle<COLOR, PERCENT, RPM>  
OR: ColorCycle<COLOR, PERCENT, RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, OFF_COLOR>  
COLOR, ON_COLOR, OFF_COLOR: COLOR  
RPM, PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number  
return value: COLOR  
This is intended for a small ring of neopixels  
A section of the ring is lit at the specified color  
and rotates at the specified speed. The size of the  
lit up section is defined by "percentage".  

## [ColorSelect](https://github.com/profezzorn/ProffieOS/blob/master/styles/color_select.h)  
Usage: ColorSelect<SELECTION, TRANSITION, COLOR1, COLOR2, ...>  
SELECTION: function  
TRANSITION: transition  
COLOR1, COLOR2, ...:  COLOR  
Return value: COLOR  
Decides what color to return based on the current selection.  
The returned color will be selection % N (where N is the number of colors arguments).  
When the selection changes, the transition will be used to change from the old color to the new color.  

## [ColorChange](https://github.com/profezzorn/ProffieOS/blob/master/styles/colorchange.h)  
Usage: ColorChange<TRANSITION, COLOR1, COLOR2, ...>  
TRANSITION: transition  
COLOR1, COLOR2, ...:  COLOR  
Return value: COLOR  
Decides what color to return based on the current variation.  
The returned color will be current_variation % N (where N is the number of colors arguments).  
When the variation changes, the transition will be used to change from the old color to the new color.  

## [Cylon](https://github.com/profezzorn/ProffieOS/blob/master/styles/cylon.h)  
Usage: Cylon<COLOR, PERCENT, RPM>  
OR: ColorCycle<COLOR, PERCENT, RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, OFF_COLOR>  
COLOR, ON_COLOR, OFF_COLOR: COLOR  
RPM, PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number  
return value: COLOR  
Cylon/Knight Rider effect, a section of the strip is  
lit up and moves back and forth. Speed, color and fraction  
illuminated can be configured separately for on and off  
states.  

## [Gradient](https://github.com/profezzorn/ProffieOS/blob/master/styles/gradient.h)  
Usage: Gradient<A, B>  
OR: Gradient<A, B, C>  
OR: Gradient<A, B, C, D, ...>  
A, B, C, D: COLOR or LAYER  
return value: COLOR or LAYER (if any of the inputs are layers)  
Gradient, color A at base, B at tip.  
Any number of colors can be put together into a gradient.  

## [HumpFlicker, HumpFlickerL](https://github.com/profezzorn/ProffieOS/blob/master/styles/hump_flicker.h)  
Usage: HumpFlicker<A, B, HUMP_WIDTH>  
OR: HumpFlickerL<B, HUMP_WIDTH>  
A, B: COLOR  
HUMP_WIDTH: a number  
return value: COLOR  
Makes a random "hump" which is about 2xHUMP_WIDTH leds wide.  

## [IgnitionDelay](https://github.com/profezzorn/ProffieOS/blob/master/styles/ignition_delay.h)  
Usage: IgnitionDelay<DELAY_MILLIS, BASE>  
DELAY_MILLIS: a number  
BASE: COLOR  
return value: COLOR  
This class renders BASE as normal, but delays ignition by  
the specified number of milliseconds. Intended for kylo-style  
quillions.  

## [InOutHelperX, InOutHelper, InOutTr, InOutTrL](https://github.com/profezzorn/ProffieOS/blob/master/styles/inout_helper.h)  
Usage: InOutHelperX<BASE, EXTENSION, OFF_COLOR>  
BASE, OFF_COLOR: COLOR  
EXTENSION: FUNCTION  
return value: COLOR  
This class does a basic extend/retract. Basically it fades between  
BASE and OFF_COLOR (which defaults to black). The amount of extension  
is determined by EXTENSION. If EXTENSION returns 32768, the blade is fully  
extended. If it returns zero, it is not extended.  

Usage: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS>  
OR: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS, OFF_COLOR>  
BASE, OFF_COLOR: COLOR  
OUT_MILLIS, IN_MILLIS: a number  
return value: COLOR  
This class does a basic extend/retract. Basically it fades between  
BASE and OFF_COLOR (which defaults to black). It starts by just  
displaying OFF_COLOR, and when you turn the saber on it starts mixing  
in BASE at the base of the saber. After OUT_MILLIS milliseconds, it  
will be displaying the BASE color on the entire blade.  

Usage: InOutTr<BASE, OUT_TRANSITION, IN_TRANSITION, OFF_COLOR>  
OR: InOutTrL<OUT_TRANSITION, IN_TRANSITION, OFF_COLOR>
BASE, OFF_COLOR: COLOR  
OUT_TRANSITION, IN_TRANSITION: TRANSITION  
return value: COLOR  
Similar to InOutHelper<>, but uses configuratble transitions  
to go to and from the BASE to the OFF_COLOR.  

## [inout_sparktip](https://github.com/profezzorn/ProffieOS/blob/master/styles/inout_sparktip.h)  
Usage: InOutSparkTip<BASE, OUT_MILLIS, IN_MILLIS, SPARK_COLOR>  
BASE, SPARK_COLOR: COLOR  
OUT_MILLIS, IN_MILLIS: a number  
return value: COLOR  
Similar to InOutHelper, but makes the tip a different color  
during extension.  

## [Layers](https://github.com/profezzorn/ProffieOS/blob/master/styles/layers.h)  
Usage: Layers<BASE, LAYER1, LAYER2, ...>  
BASE: COLOR or LAYER  
LAYER1, LAYER2: LAYER  
return value: COLOR or LAYER (same as BASE)  
This style works like layers in gimp or photoshop.  
In most cases, the layers are expected to be normally transparent effects  
that turn opaque when then want to paint an effect over the base color.  
If the base color is opqaque, the final result of this style will also be  
opaque. If the base color is transparent, the final result may also be transparent,  
depending on what the layers paint on top of the base color.  

## [LengthFinder](https://github.com/profezzorn/ProffieOS/blob/master/styles/length_finder.h)  
Usage: LengthFinder<BASE, LIGHTUP>  
OR: LengthFinder<>  
BASE, LIGHTUP: COLOR  
Return value: COLOR  
Lights up exactly one led, based on the current color change  
variable. When changed, says what the current color change is  
so that you know which led is lit up.  
Use this when you don't know how many LEDs are in your blade.  
Set the blade length to 144, enter color change mode and  
change it until no LED turns on, go back one and there you go!  

## [Lockup, LockupL, LockupTr, LockupTrL](https://github.com/profezzorn/ProffieOS/blob/master/styles/lockup.h)  
Usage: Lockup<BASE, LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE>  
OR: LockupL<LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE, LB_SHAPE>  
BASE, LOCKUP: COLOR  
DRAG_COLOR: COLOR (defaults to the LOCKUP color)  
LOCKUP_SHAPE: FUNCTION (defaults to Int<32768>)  
DRAG_SHAPE: FUNCTION (defaults to SmoothStep<Int<28671>, Int<4096>>)  
LB_SHAPE: FUNCTION (defaults to a suitable function)  
return value: COLOR  
Shows LOCKUP if the lockup state is true, otherwise BASE.  
Also handles Drag, Melt and Lightning Block lockup types unless those  
are handled elsewhere in the same style.  

Usage: LockupTr<BASE, COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION>  
OR: LockupTrL<COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION>  
COLOR; COLOR or LAYER  
BeginTr, EndTr: TRANSITION  
LOCKUP_TYPE: a SaberBase::LockupType  
Return type: LAYER  
This layer creates a complete lockup effect.  
When lockup is initiated, BeginTr is used to transition from transparent  
to COLOR. When lockup ends, EndTr is used to transition from COLOR to  
transparent again. If you wish to for your lockup to have a shape, you  
can have COLOR be partially transparent to make the base layer show through.  
If CONDITION equals 0, Lockup effect ignored  

## [Mix](https://github.com/profezzorn/ProffieOS/blob/master/styles/mix.h)  
Usage: Mix<F, A, B>  
Mix between A and B using function F  
F: INTEGER  
A, B: COLOR  
return value: COLOR or LAYER (if A or B is a layer)  
F = 0 -> return A  
F = 16384 -> return (A+B)/2  
F = 32768 -> return B  

## [OnSpark, OnSparkX, OnSparkL](https://github.com/profezzorn/ProffieOS/blob/master/styles/on_spark.h)  
Usage: OnSpark<BASE, SPARK_COLOR, MILLIS>  
OR: OnSparX<BASE, SPARK_COLOR, MILLI_CLASS>  
OR: OnSparL<SPARK_COLOR, MILLI_CLASS>  
BASE: COLOR  
SPARK_COLOR: COLOR (defaults to white)  
MILLIS: a number (defaults to 200)  
MILLI_CLASS: FUNCTION (defaults to Int<200>)  
return value: COLOR  
When you turn the saber on, it starts with SPARK_COLOR, and then  
fades to BASE over a peariod of MILLIS millseconds.  

## [StylePOV, ContinuousPOV](https://github.com/profezzorn/ProffieOS/blob/master/styles/pov.h)  
Usage: StylePOV<>  
OR: StylePOV<MIN_DEGREES, MAX_DEGREES, REPEAT, MIRROR>  
MIN_DEGREES: integer (default -45)  
MAX_DEGREES: integer (default 45)  
REPEAT: bool (default false)  
MIRROR: bool (default true)  
return value: COLOR  

Usage: ContinuousPOV<>
OR: ContinuousPOV<DEGREES>
DEGREES: integer (default 90)
return value: COLOR

## [Pulsing, PulsingX, PulsingL](https://github.com/profezzorn/ProffieOS/blob/master/styles/pulsing.h)  
Usage: Pulsing<A, B, PULSE_MILLIS>  
OR: PulsingX<A, B, PULSE_MILLIS_FUNC>  
OR: PulsingL<B, PULSE_MILLIS_FUNC>  
A, B: COLOR  
PULSE_MILLIS: a number  
PULSE_MILLIS_FUNC: FUNCTION  
return value: COLOR  
Goes back and forth between COLOR1 and COLOR2.  
A full transition from COLOR1 to COLOR2 and back again takes PULSE_MILLIS milliseconds.  

## [Rainbow](https://github.com/profezzorn/ProffieOS/blob/master/styles/rainbow.h)  
Usage: Rainbow  
return value: COLOR  
Basic RGB rainbow.  

## [RandomBlink, RandomBlinkX, RandomBlinkL](https://github.com/profezzorn/ProffieOS/blob/master/styles/random_blink.h)  
Usage: RandomBlink<MILLIHZ, COLOR1, COLOR2>  
OR: RandomBlinkX<MILLIHZ_CLASS, COLOR1, COLOR2>  
OR: RandomBlinkL<MILLIHZ_CLASS, COLOR1>  
MILLIHZ: integer  
MILLHZ_CLASS: NUMBER  
COLOR1: COLOR (defaults to WHITE)  
COLOR2: COLOR (defaults to BLACK)  
return value: COLOR  
Each LED is randomly chosen as COLOR1 or COLOR2, then stays  
that color for 1000/MILLIHZ seconds.  

## [RandomFlicker, RandomL](https://github.com/profezzorn/ProffieOS/blob/master/styles/random_flicker.h)  
Usage: RandomFlicker<A, B>  
OR: RandomL\<B>  
A, B: COLOR  
return value: COLOR  
Mixes randomly between A and B.  
mix is even over entire blade.  

## [RandomPerLEDFlicker, RandomPerLEDFlickerL](https://github.com/profezzorn/ProffieOS/blob/master/styles/random_per_led_flicker.h)  
Usage: RandomPerLEDFlicker<A, B>  
OR: RandomPerLEDFlickerL\<B>  
A, B: COLOR  
return value: COLOR  
Mixes randomly between A and B.  
mix is chosen individually for every LED.  

## [Remap](https://github.com/profezzorn/ProffieOS/blob/master/styles/remap.h)  
Usage: Remap<F, COLOR>  
F: FUNCTION - the remapping function  
COLOR: COLOR - color values to remap  
Returns: COLOR  

## [Responsive Styles](https://github.com/profezzorn/ProffieOS/blob/master/styles/responsive_styles.h)  
Usage: ResponsiveLockupL<LOCKUP COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>  
Implements LocalizedLockup that will move based on the angle of the blade  
TRANSITION1 & TRANSITION2 = transition Begin & End  
TOP = uppermost lockup position limit, BOTTOM = lowermost lockup position limit, 32768 = tip, 0 = hilt  
SIZE controls LOCKUP area size 0 ~ 32768  

Usage: ResponsiveDragL<DRAG COLOR, TRANSTION1, TRANSITION2, SIZE1, SIZE2>  
Implements Drag that will increase or decrease in size based on turning hilt  
TRANSITION1 & TRANSITION2 = transition Begin & End  
SIZE1 & SIZE2 control limits for DRAG size with TwistAngle  
LOCATION controls SmoothStep location  

Usage: ResponsiveMeltL<MELT COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>  
Implements Melt effect for cutting through object, size will change to mimic metal  
heating and intensity will increase or decrease based on turning hilt  
TRANSITION1 & TRANSITION2 = transition Begin & End  
SIZE1 & SIZE2 control MELT area limits for TwistAngle  
LOCATION control SmoothStep location  

Usage: ResponsiveLightningBlockL<LIGHTNING BLOCK COLOR, TRANSITION1, TRANSITION2>  
Implements hybrid Force Lightning Block with animation, intensity responds to turning the hilt and location/focus will respond to blade angle  
TRANSITION1 & TRANSITION2 = transition Begin & End  

Usage: ResponsiveClashL<CLASH COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>  
Implements LocalizedClash effect that mimics ResponsiveLockup location and size  
TRANSITION1 & TRANSITION2 = transition Begin & End  
TOP = uppermost Clash position limit, BOTTOM = lowermost Clash position limit, 32768 = tip, 0 = hilt  
SIZE controls Clash area size 0 ~ 32768  

Usage: ResponsiveBlastL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>  
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and disperse along the blade from original position  
FADE = fade time ms  
WAVE_SIZE = size  
WAVE MS = speed ms  
TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt  
EFFECT = effect type, defaults to EFFECT_BLAST  

Usage: ResponsiveBlastWaveL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>  
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and split up and down the length of the blade from original position  
FADE = fade time ms  
WAVE_SIZE = size  
WAVE MS = speed ms  
TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt  
EFFECT = effect type, defaults to EFFECT_BLAST  

Usage: ResponsiveBlastFadeL<BLAST COLOR, SIZE, FADE, TOP, BOTTOM, EFFECT>  
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and Fade in position  
SIZE controls blast size bump 0 ~ 32768  
FADE = fade time ms  
TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt  
EFFECT = effect type, defaults to EFFECT_BLAST  

Usage: ResponsiveStabL<STAB COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>  
Stab effect  
Implements Stab effect that will change in size based on angle of the blade  
TRANSITION1 & TRANSITION2 = transition Begin & End  
SIZE1 & SIZE2 control Stab area limits for BladeAngle, 0 ~ 32768  
LOCATION control SmoothStep location  

## [RetractionDelay](https://github.com/profezzorn/ProffieOS/blob/master/styles/retraction_delay.h)  
Usage: RetractionDelay<DELAY_MILLIS, BASE>  
DELAY_MILLIS: a number  
BASE: COLOR  
return value: COLOR  
This class renders BASE as normal, but delays retraction by  
the specified number of milliseconds.  

## [Rgb](https://github.com/profezzorn/ProffieOS/blob/master/styles/rgb.h)  
Usage: Rgb<R, G, B>  
R, G, B: a number (0-255)  
return value: COLOR  

## [RgbArg](https://github.com/profezzorn/ProffieOS/blob/master/styles/rgb_arg.h)  
Usage: RgbArg<ARG, DEFAULT_COLOR>  
ARG: a number  
DEFAULT_COLOR: Must be Rgb<> or Rgb16<>  
Return value: COLOR  
This is used to create templates that can be configured dynamically.  
These templates can be assigned to presets from WebUSB or bluetooth.  
See [style_parser](https://github.com/profezzorn/ProffieOS/blob/master/styles/style_parser.h) for more details.  

## [RgbCycle](https://github.com/profezzorn/ProffieOS/blob/master/styles/rgb_cycle.h)  
Usage: RgbCycle  
(no arguments)  
return value: COLOR  
Very fast Red, Green, Blue cycle, result should essentially be white  
until you start swinging it around.  

## [RotateColorsX](https://github.com/profezzorn/ProffieOS/blob/master/styles/rotate_color.h)  
Usage: RotateColorsX<ROTATION, COLOR>  
ROTATION: FUNCTION  
COLOR: COLOR or LAYER  
return value: COLOR or LAYER (same as COLOR)  
ROTATION specifies how much to rotate the color in HSV (color wheel)  
space. 0 = none, 32768 = 360degrees  

## [Sequence](https://github.com/profezzorn/ProffieOS/blob/master/styles/sequence.h)  
Usage: Sequence<COLOR1, COLOR2, int millis_per_bits, int bits, 0b0000000000000000, ....>  
COLOR1: COLOR  
COLOR2: COLOR  
millis_per_bit: millseconds spent on each bit  
bits: number of bits before we loop around to the beginning  
0b0000000000000000: 16-bit binary numbers containing the actual sequence.  
Shows COLOR1 if the current bit in the sequence is 1, COLOR2 otherwise.  
The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.  
Note that if not all bits are used within the 16-bit number.  
Example, a red SOS pattern:  
Sequence<RED, BLACK, 100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>  

## [Sparkle, SparkleL](https://github.com/profezzorn/ProffieOS/blob/master/styles/sparkle.h)  
Usage: Sparkle<BASE, SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>  
OR: SparkleL<SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>  
BASE: COLOR  
SPARKLE_COLOR: COLOR (defaults to white)  
SPARK_CHANCE_PROMILLE: a number  
SPARK_INTENSITY: a number  
Generally displays BASE, but creates little sparkles of SPARKLE_COLOR  
SPARK_CHANCE_PROMILLE decides how often a spark is generated, defaults to 300 (30%)  
SPARK_INTENSITY specifies how intens the spark is, defaults to 1024  

## [Stripes, StripesX](https://github.com/profezzorn/ProffieOS/blob/master/styles/stripes.h)  
Usage: Stripes<WIDTH, SPEED, COLOR1, COLOR2, ... >  
OR: Usage: StripesX<WIDTH_CLASS, SPEED, COLOR1, COLOR2, ... >  
WIDTH: integer (start with 1000, then adjust up or down)  
WIDTH_CLASS: INTEGER  
SPEED: integer  (start with 1000, then adjust up or down)  
COLOR1, COLOR2: COLOR  
return value: COLOR  
Works like rainbow, but with any colors you like.  
WIDTH determines width of stripes  
SPEED determines movement speed  

## [Strobe, StrobeX, StrobeL](https://github.com/profezzorn/ProffieOS/blob/master/styles/strobe.h)  
Usage: Strobe<BASE, STROBE_COLOR, STROBE_FREQUENCY, STROBE_MILLIS>  
OR: StrobeX<BASE, STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>  
OR: StrobeL<STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>  
BASE, STROBE_COLOR: COLOR  
STROBE_FREQUENCY, STROBE_MILLIS: a number  
STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION  
return value: COLOR  
Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS  
STROBE_FREQUENCY times per second.  

## [StylePtr](https://github.com/profezzorn/ProffieOS/blob/master/styles/style_ptr.h)  
Usage: StylePtr<BLADE>  
BLADE: COLOR  
return value: suitable for preset array  
Most blade styls are created by taking a blade style template and wrapping it  
this class, which implements the BladeStyle interface. We do this so that the  
getColor calls will be inlined in this loop for speed.  

## [TransitionEffect, TransitionEffectL](https://github.com/profezzorn/ProffieOS/blob/master/styles/transition_effect.h)  
Usage: TransitionEffect<COLOR, EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>  
OR: TransitionEffectL<EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>  
COLOR, EFFECT_COLOR: COLOR  
TRANSITION1, TRANSITION2 : TRANSITION  
EFFECT: effect type  
return value: COLOR  
When the specified EFFECT happens (clash/blast/etc.) transition from COLOR to  
EFFECT_COLOR using TRANSITION1. Then transition back using TRANSITION2.  

## [TransitionLoop, TransitionLoopL](https://github.com/profezzorn/ProffieOS/blob/master/styles/transition_loop.h)  
Usage: TransitionLoop<COLOR, TRANSITION>  
OR: TransitionLoopL<TRANSITION>  
COLOR: COLOR  
TRANSITION : TRANSITION  
return value: COLOR  
Continuously transitions COLOR to COLOR  
Makes more sense if TRANSITION is a TrConcat, as this will  
transition to/from the intermediate steps in a loop.  

## [TransitionPulseL](https://github.com/profezzorn/ProffieOS/blob/master/styles/transition_pulse.h)  
Usage: TransitionPulseL<TRANSITION, PULSE>  
TRANSITION: TRANSITION  
PULSE: FUNCTION  
return value: COLOR  
When the specified PULSE happens TRANSITION layer will run.  

