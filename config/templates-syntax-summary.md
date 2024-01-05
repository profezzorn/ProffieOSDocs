---
title: Template Syntax Summary
---

Here’s a summary list of all of the "Usage: " comment sections from the header files for  
styles, transitions, and functions as of ProffieOS 7.13.

For example, if you were looking for what arguments TrSparkX<> takes,  
now you’d know that it takes TrSparkX< COLOR, SPARK_SIZE, SPARK_MS, SPARK_CENTER>.


# Styles
```cpp
File: ./alpha.h
// Usage: AlphaL<COLOR, ALPHA>
    // COLOR: COLOR or LAYER
    // ALPHA: FUNCTION
    // Return value: LAYER
    // This function makes a color transparent. The ALPHA function specifies just how opaque it should be.
    // If ALPHA is zero, the returned color will be 100% transparent. If Alpha is 32768, the returned color will
    // be 100% opaque. Note that if COLOR is already transparent, it will be made more transparent. Example:
    // If COLOR is 50% opaque, and ALPHA returns 16384, the result will be 25% opaque.

File: ./audio_flicker.h
// Usage: AudioFlicker<A, B>
    // Or: AudioFlickerL<B>
    // A, B: COLOR
    // return value: COLOR
    // Mixes between A and B based on audio. Quiet audio
    // means more A, loud audio means more B.
    // Based on a single sample instead of an average to make it flicker.

File: ./blade_shortener.h

File: ./blade_style.h

File: ./blast.h
// Usage: Blast<BASE, BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>
    // Or: BlastL<BLAST, FADEOUT_MS, WAVE_SIZE, WAVE_MS>
    // BASE, BLAST: COLOR
    // FADEOUT_MS: a number (defaults to 150)
    // WAVE_SIZE: a number (defaults to 100)
    // WAVE_MS: a number (defaults to 400)
    // return value: COLOR
    // Normally shows BASE, but creates a blast effect using
    // the color BLAST when a blast is requested. The effect
    // is basically two humps moving out from the blast location.
    // The size of the humps can be changed with WAVE_SIZE, note
    // that smaller values makes the humps bigger. WAVE_MS determines
    // how fast the waves travel. Smaller values makes the waves
    // travel slower. Finally FADEOUT_MS determines how fast the
    // humps fade back to the base color.
// Usage: OriginalBlast<BASE, BLAST>
    // Or: OriginalBlastL<BLAST>
    // BASE, BLAST: COLOR
    // return value: COLOR
    // Normally shows BASE, but creates a blast effect using
    // the color BLAST when a blast is requested.
    // This was the original blast effect, but it is slow and not
    // very configurable.

File: ./blinking.h
// Usage: Blinking<A, B, BLINK_MILLIS, BLINK_PROMILLE>
    // or: BlinkingX<A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>
    // or: BlinkingL<B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>
    // A, B: COLOR
    // BLINK_MILLIS: a number
    // BLINK_PROMILLE: a number, defaults to 500
    // BLINK_MILLIS_FUNC: FUNCTION
    // BLINK_PROMILLE_FUNC: FUNCTION
    // return value: COLOR
    // Switches between A and B.
    // A full cycle from A to B and back again takes BLINK_MILLIS milliseconds.
    // If BLINK_PROMILLE is 500, we select A for the first half and B for the
    // second half. If BLINK_PROMILLE is smaller, we get less A and more B.
    // If BLINK_PROMILLE is 0, we get all B.
    // If BLINK_PROMILLE is 1000 we get all A.
    //

File: ./brown_noise_flicker.h
// Usage: BrownNoiseFlicker<A, B, grade>
    // Or: BrownNoiseFlickerL<B, grade>
    // A, B: COLOR
    // grade: int
    // return value: COLOR
    // Randomly selects between A and B, but keeps nearby
    // pixels looking similar.

File: ./byteorder.h
// Usage: ByteOrderStyle<BYTEORDER, COLOR>
    // BYTEORDER: Color8::RGB, or one of the other byte orders
    // COLOR: COLOR
    // return value: COLOR

File: ./charging.h
// Usage: &style_charging
    // return value: POINTER
    // Charging blade style.
    // Slowly pulsating battery indicator.

File: ./clash.h
// Usage: SimpleClash<BASE, CLASH_COLOR, CLASH_MILLIS>
    // Or: SimpleClashL<CLASH_COLOR, CLASH_MILLIS>
    // BASE: COLOR
    // CLASH_COLOR: COLOR (defaults to white)
    // CLASH_MILLIS: a number (defaults to 40)
    // return value: COLOR
    // Turns the blade to CLASH_COLOR for CLASH_MILLIS millseconds
    // when a clash occurs.
// Usage: LocalizedClash<BASE, CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>
    // Usage: LocalizedClashL<CLASH_COLOR, CLASH_MILLIS, CLASH_WIDTH_PERCENT=50>
    // BASE: COLOR
    // CLASH_COLOR: COLOR (defaults to white)
    // CLASH_MILLIS: a number (defaults to 40)
    // return value: COLOR
    // Similar to SimpleClash, but lights up a portion of the blade.
    // The fraction of the blade is defined by CLASH_WIDTH_PERCENT
    // The location of the clash is random within the middle half of the blade.
    // Localized clashes should work well with stabs with no modifications.

File: ./color_cycle.h
// Usage: ColorCycle<COLOR, PERCENT, RPM>
    // or: ColorCycle<COLOR, PERCENT, RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, OFF_COLOR>
    // COLOR, ON_COLOR, OFF_COLOR: COLOR
    // RPM, PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number
    // return value: COLOR
    // This is intended for a small ring of neopixels
    // A section of the ring is lit at the specified color
    // and rotates at the specified speed. The size of the
    // lit up section is defined by "percentage".

File: ./color_select.h
// Usage: ColorSelect<SELECTION, TRANSITION, COLOR1, COLOR2, ...>
    // SELECTION: function
    // TRANSITION: transition
    // COLOR1, COLOR2, ...:  COLOR
    // Return value: COLOR
    // Decides what color to return based on the current selection.
    // The returned color will be selection % N (where N is the number of colors arguments).
    // When the selection changes, the transition will be used to change from the old color to the new color.

File: ./colorchange.h
// Usage: ColorChange<TRANSITION, COLOR1, COLOR2, ...>
    // TRANSITION: transition
    // COLOR1, COLOR2, ...:  COLOR
    // Return value: COLOR
    // Decides what color to return based on the current variation.
    // The returned color will be current_variation % N (where N is the number of colors arguments).
    // When the variation changes, the transition will be used to change from the old color to the new color.

File: ./colors.h

File: ./cylon.h
// Usage: Cylon<COLOR, PERCENT, RPM>
    // or: ColorCycle<COLOR, PERCENT, RPM, ON_COLOR, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS, OFF_COLOR>
    // COLOR, ON_COLOR, OFF_COLOR: COLOR
    // RPM, PERCENT, ON_PERCENT, ON_RPM, FADE_TIME_MILLIS: a number
    // return value: COLOR
    // Cylon/Knight Rider effect, a section of the strip is
    // lit up and moves back and forth. Speed, color and fraction
    // illuminated can be configured separately for on and off
    // states.

File: ./edit_mode.h

File: ./effect_sequence.h

File: ./file.h

File: ./fire.h

File: ./gradient.h
// Usage: Gradient<A, B>
    // OR: Gradient<A, B, C>
    // OR: Gradient<A, B, C, D, ...>
    // A, B, C, D: COLOR or LAYER
    // return value: COLOR or LAYER (if any of the inputs are layers)
    // Gradient, color A at base, B at tip.
    // Any number of colors can be put together into a gradient.

File: ./hump_flicker.h
// Usage: HumpFlicker<A, B, HUMP_WIDTH>
    // Or: HumpFlickerL<B, HUMP_WIDTH>
    // A, B: COLOR
    // HUMP_WIDTH: a number
    // return value: COLOR
    // Makes a random "hump" which is about 2xHUMP_WIDTH leds wide.

File: ./ignition_delay.h
// Usage: IgnitionDelay<DELAY_MILLIS, BASE>
    // DELAY_MILLIS: a number
    // BASE: COLOR
    // return value: COLOR
    // This class renders BASE as normal, but delays ignition by
    // the specified number of milliseconds. Intended for kylo-style
    // quillions.

File: ./inout_helper.h
// Usage: InOutHelperX<BASE, EXTENSION, OFF_COLOR>
    // BASE, OFF_COLOR: COLOR
    // EXTENSION: FUNCTION
    // return value: COLOR
    // This class does a basic extend/retract. Basically it fades between
    // BASE and OFF_COLOR (which defaults to black). The amount of extension
    // is determined by EXTENSION. If EXTENSION returns 32768, the blade is fully
    // extended. If it returns zero, it is not extended.
// Usage: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS>
    // or: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS, OFF_COLOR>
    // BASE, OFF_COLOR: COLOR
    // OUT_MILLIS, IN_MILLIS: a number
    // return value: COLOR
    // This class does a basic extend/retract. Basically it fades between
    // BASE and OFF_COLOR (which defaults to black). It starts by just
    // displaying OFF_COLOR, and when you turn the saber on it starts mixing
    // in BASE at the base of the saber. After OUT_MILLIS milliseconds, it
    // will be displaying the BASE color on the entire blade.
// Usage: InOutTr<BASE, OUT_TRANSITION, IN_TRANSITION, OFF_COLOR>
    // BASE, OFF_COLOR: COLOR
    // OUT_TRANSITION, IN_TRANSITION: TRANSITION
    // return value: COLOR
    // Similar to InOutHelper<>, but uses configuratble transitions
    // to go to and from the BASE to the OFF_COLOR.

File: ./inout_sparktip.h
// Usage: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS>
    // or: InOutHelper<BASE, OUT_MILLIS, IN_MILLIS, SPARK_COLOR>
    // BASE, SPARK_COLOR: COLOR
    // OUT_MILLIS, IN_MILLIS: a number
    // return value: COLOR
    // Similar to InOutHelper, but makes the tip a different color
    // during extension.

File: ./layers.h
// Usage: Layers<BASE, LAYER1, LAYER2, ...>
    // BASE: COLOR or LAYER
    // LAYER1, LAYER2: LAYER
    // return value: COLOR or LAYER (same as BASE)
    // This style works like layers in gimp or photoshop.
    // In most cases, the layers are expected to be normally transparent effects
    // that turn opaque when then want to paint an effect over the base color.
    // If the base color is opqaque, the final result of this style will also be
    // opaque. If the base color is transparent, the final result may also be transparent,
    // depending on what the layers paint on top of the base color.

File: ./legacy_styles.h

File: ./length_finder.h
// Usage: LengthFinder<BASE, LIGHTUP>
    // or: LengthFinder<>
    // BASE, LIGHTUP: COLOR
    // Return value: COLOR
    // Lights up exactly one led, based on the current color change
    // variable. When changed, says what the current color change is
    // so that you know which led is lit up.
    // Use this when you don't know how many LEDs are in your blade.
    // Set the blade length to 144, enter color change mode and
    // change it until no LED turns on, go back one and there you go!

File: ./lockup.h
// Usage: Lockup<BASE, LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE>
    // Or: LockupL<LOCKUP, DRAG_COLOR, LOCKUP_SHAPE, DRAG_SHAPE, LB_SHAPE>
    // BASE, LOCKUP: COLOR
    // DRAG_COLOR: COLOR (defaults to the LOCKUP color)
    // LOCKUP_SHAPE: FUNCTION (defaults to Int<32768>)
    // DRAG_SHAPE: FUNCTION (defaults to SmoothStep<Int<28671>, Int<4096>>)
    // LB_SHAPE: FUNCTION (defaults to a suitable function)
    // return value: COLOR
    // Shows LOCKUP if the lockup state is true, otherwise BASE.
    // Also handles Drag, Melt and Lightning Block lockup types unless those
    // are handled elsewhere in the same style.
// Usage: LockupTr<BASE, COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION>
    // Or: LockupTrL<COLOR, BeginTr, EndTr, LOCKUP_TYPE, CONDITION>
    // COLOR; COLOR or LAYER
    // BeginTr, EndTr: TRANSITION
    // LOCKUP_TYPE: a SaberBase::LockupType
    // Return type: LAYER
    // This layer creates a complete lockup effect.
    // When lockup is initiated, BeginTr is used to transition from transparent
    // to COLOR. When lockup ends, EndTr is used to transition from COLOR to
    // transparent again. If you wish to for your lockup to have a shape, you
    // can have COLOR be partially transparent to make the base layer show through.
    // If CONDITION equals 0, Lockup effect ignored

File: ./mix.h
// Usage: Mix<F, A, B>
    // Mix between A and B using function F
    // F: INTEGER
    // A, B: COLOR
    // return value: COLOR or LAYER (if A or B is a layer)
    //
    // F = 0 -> return A
    // F = 16384 -> return (A+B)/2
    // F = 32768 -> return B

File: ./on_spark.h
// Usage: OnSpark<BASE, SPARK_COLOR, MILLIS>
    // Or: OnSparX<BASE, SPARK_COLOR, MILLI_CLASS>
    // Or: OnSparL<SPARK_COLOR, MILLI_CLASS>
    // BASE: COLOR
    // SPARK_COLOR: COLOR (defaults to white)
    // MILLIS: a number (defaults to 200)
    // MILLI_CLASS: FUNCTION (defaults to Int<200>)
    // return value: COLOR
    // When you turn the saber on, it starts with SPARK_COLOR, and then
    // fades to BASE over a peariod of MILLIS millseconds.

File: ./pov.h
// Usage: StylePOV<>
    // or: StylePOV<MIN_DEGREES, MAX_DEGREES, REPEAT, MIRROR>
    // MIN_DEGREES: integer (default -45)
    // MAX_DEGREES: integer (default 45)
    // REPEAT: bool (default false)
    // MIRROR: bool (default true)
    // return value: COLOR

File: ./pulsing.h
// Usage: Pulsing<A, B, PULSE_MILLIS>
    // or: PulsingX<A, B, PULSE_MILLIS_FUNC>
    // or: PulsingL<B, PULSE_MILLIS_FUNC>
    // A, B: COLOR
    // PULSE_MILLIS: a number
    // PULSE_MILLIS_FUNC: FUNCTION
    // return value: COLOR
    // Goes back and forth between COLOR1 and COLOR2.
    // A full transition from COLOR1 to COLOR2 and back again takes PULSE_MILLIS milliseconds.

File: ./rainbow.h
// Usage: Rainbow
    // return value: COLOR
    // Basic RGB rainbow.

File: ./random_blink.h
// usage: RandomBlink<MILLIHZ, COLOR1, COLOR2>
    // or: RandomBlinkX<MILLIHZ_CLASS, COLOR1, COLOR2>
    // or: RandomBlinkL<MILLIHZ_CLASS, COLOR1>
    // MILLIHZ: integer
    // MILLHZ_CLASS: NUMBER
    // COLOR1: COLOR (defaults to WHITE)
    // COLOR2: COLOR (defaults to BLACK)
    // return value: COLOR
    // Each LED is randomly chosen as COLOR1 or COLOR2, then stays
    // that color for 1000/MILLIHZ seconds.

File: ./random_flicker.h
// Usage: RandomFlicker<A, B>
    // Or: RandomL<B>
    // A, B: COLOR
    // return value: COLOR
    // Mixes randomly between A and B.
    // mix is even over entire blade.

File: ./random_per_led_flicker.h
// Usage: RandomPerLEDFlicker<A, B>
    // Or: RandomPerLEDFlickerL<B>
    // A, B: COLOR
    // return value: COLOR
    // Mixes randomly between A and B.
    // mix is chosen individually for every LED.

File: ./remap.h
// Usage: Remap<F,COLOR>
    // F: FUNCTION - the remapping function
    // COLOR: COLOR - color values to remap
    // Returns: COLOR

File: ./responsive_styles.h
// Usage: ResponsiveLockupL<LOCKUP COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>
    // Implements LocalizedLockup that will move based on the angle of the blade
    // TRANSITION1 & TRANSITION2 = transition Begin & End
    // TOP = uppermost lockup position limit, BOTTOM = lowermost lockup position limit, 32768 = tip, 0 = hilt
    // SIZE controls LOCKUP area size 0 ~ 32768
// Usage: ResponsiveDragL<DRAG COLOR, TRANSTION1, TRANSITION2, SIZE1, SIZE2>
    // Implements Drag that will increase or decrease in size based on turning hilt
    // TRANSITION1 & TRANSITION2 = transition Begin & End
    // SIZE1 & SIZE2 control limits for DRAG size with TwistAngle
    // LOCATION controls SmoothStep location
// Usage: ResponsiveMeltL<MELT COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>
    // Implements Melt effect for cutting through object, size will change to mimic metal
    // heating and intensity will increase or decrease based on turning hilt
    // TRANSITION1 & TRANSITION2 = transition Begin & End
    // SIZE1 & SIZE2 control MELT area limits for TwistAngle
    // LOCATION control SmoothStep location
// Usage: ResponsiveLightningBlockL<LIGHTNING BLOCK COLOR, TRANSITION1, TRANSITION2>
    // Implements hybrid Force Lightning Block with animation, intensity responds to turning the hilt and location/focus will respond to blade angle
    // TRANSITION1 & TRANSITION2 = transition Begin & End
// Usage: ResponsiveClashL<CLASH COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>
    // Implements LocalizedClash effect that mimics ResponsiveLockup location and size
    // TRANSITION1 & TRANSITION2 = transition Begin & End
    // TOP = uppermost Clash position limit, BOTTOM = lowermost Clash position limit, 32768 = tip, 0 = hilt
    // SIZE controls Clash area size 0 ~ 32768
// Usage: ResponsiveBlastL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>
    // Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and disperse along the blade from original position
    // FADE = fade time ms
    // WAVE_SIZE = size
    // WAVE MS = speed ms
    // TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt
    // EFFECT = effect type, defaults to EFFECT_BLAST
// Usage: ResponsiveBlastWaveL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>
    // Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and split up and down the length of the blade from original position
    // FADE = fade time ms
    // WAVE_SIZE = size
    // WAVE MS = speed ms
    // TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt
    // EFFECT = effect type, defaults to EFFECT_BLAST
// Usage: ResponsiveBlastFadeL<BLAST COLOR, SIZE, FADE, TOP, BOTTOM, EFFECT>
    // Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and Fade in position
    // SIZE controls blast size bump 0 ~ 32768
    // FADE = fade time ms
    // TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt
    // EFFECT = effect type, defaults to EFFECT_BLAST
// Usage: ResponsiveStabL<STAB COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>
    // Stab effect
    // Implements Stab effect that will change in size based on angle of the blade
    // TRANSITION1 & TRANSITION2 = transition Begin & End
    // SIZE1 & SIZE2 control Stab area limits for BladeAngle, 0 ~ 32768
    // LOCATION control SmoothStep location

File: ./retraction_delay.h
// Usage: RetractionDelay<DELAY_MILLIS, BASE>
    // DELAY_MILLIS: a number
    // BASE: COLOR
    // return value: COLOR
    // This class renders BASE as normal, but delays retraction by
    // the specified number of milliseconds.

File: ./rgb.h
// Usage: Rgb<R, G, B>
    // R, G, B: a number (0-255)
    // return value: COLOR

File: ./rgb_arg.h
// Usage: RgbArg<ARG, DEFAULT_COLOR>
    // ARG: a number
    // DEFAULT_COLOR: Must be Rgb<> or Rgb16<>
    // Return value: COLOR
    // This is used to create templates that can be configured dynamically.
    // These templates can be assigned to presets from WebUSB or bluetooth.
    // See style_parser.h for more details.

File: ./rgb_cycle.h
// Usage: RgbCycle
    // (no arguments)
    // return value: COLOR
    // Very fast Red, Green, Blue cycle, result should essentially be white
    // until you start swinging it around.

File: ./rotate_color.h
// Usage: RotateColorsX<ROTATION, COLOR>
    // ROTATION: FUNCTION
    // COLOR: COLOR or LAYER
    // return value: COLOR or LAYER (same as COLOR)
    //
    // ROTATION specifies how much to rotate the color in HSV (color wheel)
    // space. 0 = none, 32768 = 360degrees

File: ./sequence.h
// usage: Sequence<COLOR1, COLOR2, int millis_per_bits, int bits, 0b0000000000000000, ....>
    // COLOR1: COLOR
    // COLOR2: COLOR
    // millis_per_bit: millseconds spent on each bit
    // bits: number of bits before we loop around to the beginning
    // 0b0000000000000000: 16-bit binary numbers containing the actual sequence.
    //
    // Shows COLOR1 if the current bit in the sequence is 1, COLOR2 otherwise.
    // The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.
    // Note that if not all bits are used within the 16-bit number.
    // Example, a red SOS pattern:
    // Sequence<RED, BLACK, 100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>

File: ./show_color.h

File: ./sparkle.h
// Usage: Sparkle<BASE, SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>
    // Or: SparkleL<SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>
    // BASE: COLOR
    // SPARKLE_COLOR: COLOR (defaults to white)
    // SPARK_CHANCE_PROMILLE: a number
    // SPARK_INTENSITY: a number
    // Generally displays BASE, but creates little sparkles of SPARKLE_COLOR
    // SPARK_CHANCE_PROMILLE decides how often a spark is generated, defaults to 300 (30%)
    // SPARK_INTENSITY specifies how intens the spark is, defaults to 1024

File: ./star_wars_logo_pov_data.h

File: ./stripes.h
// Usage: Stripes<WIDTH, SPEED, COLOR1, COLOR2, ... >
    // or: Usage: StripesX<WIDTH_CLASS, SPEED, COLOR1, COLOR2, ... >
    // WIDTH: integer (start with 1000, then adjust up or down)
    // WIDTH_CLASS: INTEGER
    // SPEED: integer  (start with 1000, then adjust up or down)
    // COLOR1, COLOR2: COLOR
    // return value: COLOR
    // Works like rainbow, but with any colors you like.
    // WIDTH determines width of stripes
    // SPEED determines movement speed

File: ./strobe.h
// Usage: Strobe<BASE, STROBE_COLOR, STROBE_FREQUENCY, STROBE_MILLIS>
    // or: StrobeX<BASE, STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>
    // or: StrobeL<STROBE_COLOR, STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC>
    // BASE, STROBE_COLOR: COLOR
    // STROBE_FREQUENCY, STROBE_MILLIS: a number
    // STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION
    // return value: COLOR
    // Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS
    // STROBE_FREQUENCY times per second.

File: ./style_parser.h

File: ./style_ptr.h
// Usage: StylePtr<BLADE>
    // BLADE: COLOR
    // return value: suitable for preset array
    // Most blade styls are created by taking a blade style template and wrapping it
    // this class, which implements the BladeStyle interface. We do this so that the
    // getColor calls will be inlined in this loop for speed.

File: ./transition_effect.h
// Usage: TransitionEffect<COLOR, EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>
    // Or: TransitionEffectL<EFFECT_COLOR, TRANSITION1, TRANSITION2, EFFECT>
    // COLOR, EFFECT_COLOR: COLOR
    // TRANSITION1, TRANSITION2 : TRANSITION
    // EFFECT: effect type
    // return value: COLOR
    //
    // When the specified EFFECT happens (clash/blast/etc.) transition from COLOR to
    // EFFECT_COLOR using TRANSITION1. Then transition back using TRANSITION2.

File: ./transition_loop.h
// Usage: TransitionLoop<COLOR, TRANSITION>
    // Or: TransitionLoopL<TRANSITION>
    // COLOR: COLOR
    // TRANSITION : TRANSITION
    // return value: COLOR
    //
    // Continuously transitions COLOR to COLOR
    // Makes more sense if TRANSITION is a TrConcat, as this will
    // transition to/from the intermediate steps in a loop.

File: ./transition_pulse.h
// Usage: TransitionPulseL<TRANSITION, PULSE>
    // TRANSITION: TRANSITION
    // PULSE: FUNCTION
    // return value: COLOR
    //
    // When the specified PULSE happens TRANSITION layer will run.

```

# Transitions
```cpp
File: ./base.h

File: ./blink.h
// Usage: TrBlinkX<MILLIS_FUNCTION, N, WIDTH_FUNCTION>
    // or: TrBlink<MILLIS, N, WIDTH>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // N: a number
    // WIDTH_FUNCTION: FUNCTION, defaults to Int<16384>
    // WIDTH: a number, defaults to 16384
    // return value: TRANSITION
    // Blinks A-B N times in MILLIS, based on WIDTH (0 ~ 32768)
    // If WIDTH = 16384 A and B appear equally, lower decreases length of A, higher increases length of A

File: ./boing.h
// Usage: TrFadeX<MILLIS_FUNCTION, N>
    // or: TrFade<MILLIS, N>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // N: a number
    // return value: TRANSITION
    // Similar to TrFade, but transitions back and forth between the two
    // colors several times. (As specified by N). If N is 0, it's equal to
    // TrFade. If N is 1 it transitions A-B-A-B, if N is 2, it is A-B-A-B-A-B,
    // and so on.

File: ./center_wipe.h
// Usage: TrCenterWipeX<POSITION_FUNCTION, MILLIS_FUNCTION>
    // or: TrCenterWipe<POSITION, MILLIS>
    // POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION
    // POSITION: Int
    // MILLIS: a number
    // return value: TRANSITION
    // In the beginning entire blade is color A, then color B 
    // starts at the POSTION and extends up and down the blade
    // in the specified number of milliseconds.
// Usage: TrCenterWipeInX<POSITION_FUNCTION, MILLIS_FUNCTION>
    // or: TrCenterWipeIn<POSITION, MILLIS>
    // POSITION_FUNCTION & MILLIS_FUNCTION: FUNCTION
    // POSITION: Int
    // MILLIS: a number
    // return value: TRANSITION
    // In the beginning entire blade is color A, then color B 
    // starts at the ends and moves toward POSITION
    // in the specified number of milliseconds.

File: ./colorcycle.h
// Usage: TrColorCycle<MILLIS, START_RPM, END_RPM>
    // MILLS:  number
    // START_RPM: a number (defaults to 0)
    // END_RPM: a number (defaults to 6000)
    // return value: COLOR
    // Tron-like transition.

File: ./concat.h
// Usage: TrConcat<TRANSITION, INTERMEDIATE, TRANSITION, ...>
    // OR:  TrConcat<TRANSITION, TRANSITION, ...>
    // TRANSITION: TRANSITION
    // INTERMEDIATE: COLOR
    // return value: TRANSITION
    // Concatenates any number of transitions.
    // If an intermediate color is provided, we first transition to that color, then
    // we transition away from it in the next transition.
    // If no intermediate color is provided, the first and second transition will both
    // transition from the same input colors. If for instance both the first and second
    // transitions are TrFades, then there will be a jump in the middle as the transition
    // will go back and start from the beginning. Using TimeReverseX on the second transition
    // will avoid this, as the second transition will then run backwards.

File: ./delay.h
// Usage: TrDelayX<MILLIS_FUNCTION>
    // or: TrDelay<MILLIS>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // return value: TRANSITION
    // Waits for the specified number of milliseconds, then transitions
    // to second color. Menant to be used with TrConcat

File: ./doeffect.h
// Usage: TrDoEffectX<TRANSITION, EFFECT, WAVNUM, LOCATION_CLASS>
    // or: TrDoEffects<TRANSITION, EFFECT, WAVNUM, LOCATION>
    // TRANSITION: TRANSITION
    // EFFECT: effect type
    // WAVNUM, LOCATION: a number
    // LOCATION_CLASS: INTEGER
    // return value: TRANSITION
    // Runs the specified TRANSITION and triggers EFFECT (unless the blade is off)
    // Can specify WAV file to use for EFFECT with WAVNUM
    // NOTE: 0 is first wav file, -1 is random wav
    // LOCATION = -1 is random

File: ./extend.h
// Usage: TrExtendX<MILLIS_FUNCTION, TRANSITION>
    // or: TrExtend<MILLIS, TRANSITION>
    // MILLIS_FUNCTION: FUNCTION
    // TRANSITION: TRANSITION
    // MILLIS: a number
    // return value: TRANSITION
    // Runs the specified transition, then holds the
    // last value for some additional time specified by
    // MILLIS_FUNCTION.

File: ./fade.h
// Usage: TrFadeX<MILLIS_FUNCTION>
    // or: TrFade<MILLIS>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // return value: TRANSITION
    // Linear fading between two colors in specified number of milliseconds.
// Usage: TrSmoothFadeX<MILLIS_FUNCTION>
    // or: TrSmoothFade<MILLIS>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // return value: TRANSITION
    // Similar to TrFade, but uses a cubic fading function
    // so fading starts slow, speeds up in the middle, then
    // slows down at the end.

File: ./instant.h
// Usage: TrInstant
    // return value: TRANSITION
    // Instant transition.

File: ./join.h
// Usage: TrJoin<TR1, TR2, ...>
    // TR1, TR2: TRANSITION
    // return value: TRANSITION
    // A little hard to explain, but all the specified
    // transitions are run in parallel. Basically, we
    // chain transitions like ((A TR1 B) TR2 B)
// Usage: TrJoinR<TR1, TR2, ...>
    // TR1, TR2: TRANSITION
    // return value: TRANSITION
    // Similar to TrJoin, but transitions are chained
    // to the right instead of to the left. Like:
    // (A TR2 (A TR1 B))

File: ./loop.h
// Usage: TrLoop<TRANSITION>
    // TRANSITION: TRANSITION
    // Return Value: TRANSITION
    // Runs the specified transition in a loop forever.
// Usage: TrLoopNX<N_FUNCTION, TRANSITION>
    // or: TrLoopN<N, TRANSITION>
    // N_FUNCTION: FUNCTION (number of Loops)
    // N: a number (Loops)
    // TRANSITION: TRANSITION
    // Return Value: TRANSITION
    // Runs the specified transition N times.
// Usage: TrLoopUntil<PULSE, TRANSITION, OUT>
    // TRANSITION, OUT: TRANSITION
    // PULSE: FUNCTION (pulse)
    // Return Value: TRANSITION
    // Runs the specified transition until the pulse occurs.
    // When the pulse occurs, the loop continues, but OUT is used to
    // transition away from it, and when OUT is done, the transition is done.

File: ./random.h
// Usage: TrRandom<TR1, TR2, ...>
    // TR1, TR2: TRANSITION
    // return value: TRANSITION
    // Each time a new transition is started, a random
    // transition is picked from the specified list of
    // transitions.

File: ./select.h
// Usage: TrSelect<SELECTION, TR1, TR2, ...>
    // SELECTION: FUNCTION
    // TR1, TR2: TRANSITION
    // return value: TRANSITION
    // transition option is picked from the specified list of
    // transitions based on Int<>
    // with Int<0> representing first transition

File: ./sequence.h
// Usage: TrSequence<TR1, TR2, ...>
    // TR1, TR2: TRANSITION
    // return value: TRANSITION
    // transition options used in sequence

File: ./wave.h
// Usage: TrWaveX<COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER>
    // COLOR: COLOR
    // FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER: FUNCTIONS
    // TrWave is implements a wave traveling out from a specified point.
    // It's based on the Blast effect and is meant to look like a ripple starting
    // at a point on the blade. Unlike other transitions, this effect starts and ends
    // at the same color, and the wave is drawn using COLOR instead of the start/end
    // colors like most transitions do. It's intended to be used with TransitionLoopL
    // or TransitionEffectL, which take transitions that start and begin with the same
    // color.
// Usage: TrSparkX< COLOR, SPARK_SIZE, SPARK_MS, SPARK_CENTER>
    // COLOR: COLOR
    // SPARK_SIZE, SPARK_MS, SPARK_CENTER: FUNCTIONS
    // TrSparkX generates a wave without Fade over the length of the blade from 
    // SPARK_CENTER. Unlike other transitions, this effect starts and ends
    // at the same color, and the wave is drawn using COLOR instead of the start/end
    // colors like most transitions do. It's intended to be used with TransitionLoopL
    // or TransitionEffectL, which take transitions that start and begin with the same
    // color.

File: ./wipe.h
// Usage: TrWipeX<MILLIS_FUNCTION>
    // or: TrWipe<MILLIS>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // return value: TRANSITION
    // Similar to saber ignition. In the beginning
    // entire blade is color A, then color B starts at the base
    // and extends up to the tip of the blade in the specified
    // number of milliseconds.
// Usage: TrWipeInX<MILLIS_FUNCTION>
    // or: TrWipeIn<MILLIS>
    // MILLIS_FUNCTION: FUNCTION
    // MILLIS: a number
    // return value: TRANSITION
    // Like TrWipe, but from tip to base.
// Usage: TrWipeSparkTip<SPARK_COLOR, MILLIS, SIZE>
    // SPARK_COLOR = COLOR
    // MILLIS = a number
    // SIZE = a number
    // return value: TRANSITION
    // Same as TrWipe, but adds a "spark" tip to the
    // leading edge of the wipe color.
// Usage: TrWipeInSparkTip<SPARK_COLOR, MILLIS, SIZE>
    // SPARK_COLOR = COLOR
    // MILLIS = a number
    // SIZE = a number
    // return value: TRANSITION
    // Like TrWipeSparkTip, but from tip to base.

```

# Functions
```cpp

File: ./alt.h
// Usage: AltF
    // return value: INTEGER
    // Returns current_alternative for use in ColorSelect<>, TrSelect<> or IntSelect<>
// Usage: SyncAltToVarianceF
    // return value: INTEGER (always zero)
    // Enables Bidirectional synchronization between ALT and VARIANCE.
    // If variance changes, so does alt, if alt changes, so does variance.
// Usage: SyncAltToVarianceL
    // return value: LAYER (transparent)
    // Synchronizes alt to variance, just put it somewhere in the layer stack. (but not first)

File: ./battery_level.h
// Usage: BatteryLevel
    // Returns 0-32768 based on battery level.
    // returned value: INTEGER

File: ./blade_angle.h
// Usage: BladeAngleX<MIN, MAX>
    // Returns 0-32768 based on angle of blade
    // MIN : FUNCTION (defaults to Int<0>)
    // MAX : FUNCTION (defaults to Int<32768>)
    // MIN and MAX specifies the range of angles which are used.
    // For MIN and MAX 0 means down and 32768 means up and 16384 means
    // pointing towards the horizon.
    // So if MIN=16484 and MAX=32768, BladeAngle will return zero when you
    // point the blade towards the horizon and 32768 when you point it
    // straight up. Any angle below the horizon will also return zero.
    // returned value: FUNCTION, same for all LEDs.

File: ./blast.h
// Usage: BlastF<FADEOUT_MS, WAVE_SIZE, WAVE_MS, EFFECT>
    // FADOUT_MS: a number (defaults to 200)
    // WAVE_SIZE: a number (defaults to 100)
    // WAVE_MS: a number (defaults to 400)
    // EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)
    // returned value: FUNCTION
    // This function is intended to be used in a Mix<> or AlphaL<>
    // When a blast occurs, it makes a wave starting at the blast
    // location (which is currently random) and travels out
    // from that direction. At the peak, this function returns
    // 32768 and when there is no blast it returns zero.
    // The FADOUT_MS controls how long it takes the wave to
    // fade out. The WAVE_SIZE controls the width of the wave.
    // The WAVE_MS parameter controls the speed of the waves.
    // EFFECT can be used to trigger this effect by something
    // other than a blast effect.
// Usage: BlastFadeoutF<FADEOUT_MS, EFFECT>
    // FADEOUT_MS: a number (defaults to 250)
    // EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)
    // return value: FUNCTION
    // NOrmally returns 0, but returns up to 32768 when the
    // selected effect occurs. Then if fades back to zero over
    // FADEOUT_MS milliseconds.
// Usage: OriginalBlastF<EFFECT>
    // EFFECT: a BladeEffectType (defaults to EFFECT_BLAST)
    // return value: FUNCTION
    // Original blast function. Normally returns zero, but
    // returns up to 32768 when the selected effect occurs.

File: ./blinking.h
// Usage: BlinkingF<A, B, BLINK_MILLIS_FUNC, BLINK_PROMILLE_FUNC>
    // BLINK_MILLIS: a number
    // BLINK_PROMILLE: a number, defaults to 500
    // BLINK_MILLIS_FUNC: FUNCTION
    // BLINK_PROMILLE_FUNC: FUNCTION
    // return value: FUNCTION
    // Switches between 0 and 32768
    // A full cycle from 0 to 328768 and back again takes BLINK_MILLIS milliseconds.
    // If BLINK_PROMILLE is 500, we select A for the first half and B for the
    // second half. If BLINK_PROMILLE is smaller, we get less A and more B.
    // If BLINK_PROMILLE is 0, we get all 0.
    // If BLINK_PROMILLE is 1000 we get all 32768.
    //

File: ./brown_noise.h
// Usage: BrownNoiseF<GRADE>
    // return value: FUNCTION
    // Returns a value between 0 and 32768 with nearby pixels being similar.
    // GRADE controls how similar nearby pixels are.
// Usage: SlowNoise<SPEED>
    // return value: FUNCTION
    // Returns a value between 0 and 32768 which changes randomly up and
    // down over time. All pixels gets the same value.
    // SPEED controls how quickly the value changes.

File: ./bump.h
// Usage: Bump<BUMP_POSITION, BUMP_WIDTH_FRACTION>
    // Returns different values for each LED, forming a bump shape.
    // If BUMP_POSITION is 0, bump will be at the hilt.
    // If BUMP_POSITION is 32768, the bump will be at the tip.
    // If BUMP_WIDTH_FRACTION is 1, bump will be extremely narrow.
    // If BUMP_WIDTH_FRACTION is 32768, it will fill up most/all of the blade.
    // BUMP_POSITION, BUMP_WIDTH_FRACTION: INTEGER
// Usage: HumpFlickerFX<FUNCTION>
    // or: HumpFlickerF<N>
    // FUNCTION: FUNCTION
    // N: NUMBER
    // return value: INTEGER
    // Creates hump shapes that randomize over the blade.
    // The returned INTEGER is the size of the humps.
    // Large values can give the blade a shimmering look, 
    // while small values look more like speckles.

File: ./center_dist.h
// Usage: Remap<CenterDistF<CENTER>,COLOR>
    // Distributes led COLOR from CENTER
    // CENTER : FUNCTION (defaults to Int<16384>)

File: ./change_slowly.h
// Usage: ChangeSlowly<F, SPEED>
    // Changes F by no more than SPEED values per second.
    // F, SPEED: FUNCTION
    // return value: FUNCTION, same for all LEDs

File: ./circular_section.h
// Usage: CircularSectionF<POSITION, FRACTION>
    // POSITION: FUNCTION position on the circle or blade, 0-32768
    // FRACTION: FUNCTION how much of the blade to light up, 0 = none, 32768 = all of it
    // return value: FUNCTION
    // Returns 32768 for LEDs near the position with wrap-around.
    // Could be used with MarbleF<> for a marble effect, or with
    // Saw<> for a spinning/colorcycle type effect.
    // Example: If POSITION = 0 and FRACTION = 16384, then this function
    // will return 32768 for the first 25% and the last 25% of the blade
    // and 0 for the rest of the LEDs.

File: ./clamp.h
// Usage: ClampF<F, MIN, MAX>
    // Or:    ClampFX<F, MINCLASS, MAXCLASS>
    // Clamps value between MIN and MAX
    // F, MIN, MAX: INTEGER
    // MINCLASS, MAXCLASS: FUNCTION
    // return value: INTEGER

File: ./clash_impact.h
// Usage: ClashImpactFX<MIN, MAX>
    // MIN is minimum value Clash is detected (recommended range 0 ~ 500, default is 200)
    // MAX is maximum impact to return 32768 (recommended range 1000 ~ 1600, default is 1600)
    // Returns 0-32768 based on impact strength of clash
    // returned value: INTEGER

File: ./divide.h
// Usage: Divide<F, V>
    // Divide F by V
    // If V = 0, returns 0
    // F, V: FUNCTION, 
    // return value: FUNCTION
    // Please note that Divide<> isn't an exact inverse of Mult<> because mult uses fixed-point mathematics
    // (it divides the result by 32768) while Divide<> doesn't, it just returns F / V

File: ./effect_increment.h
// Usage: EffectPulse<EFFECT>
    // EFFECT: BladeEffectType
    // Returns 32768 once for each time the given effect occurs.
// Usage: LockupPulseF<LOCKUP_TYPE>
    // LOCKUP_TYPE: a SaberBase::LockupType
    // Returns 32768 once for each time the given lockup occurs.
// Usage: IncrementWithReset<PULSE, RESET_PULSE, MAX, I>
    // PULSE: FUNCTION (pulse type) 
    // RESET_PULSEE: FUNCTION (pulse type) defaults to Int<0> (no reset)
    // MAX, I: FUNCTION
    // Starts at zero, increments by I each time the PULSE occurse.
    // If it reaches MAX it stays there.
    // Resets back to zero when RESET_PULSE occurs.
// Usage: EffectIncrementF<EFFECT, MAX, I>
    // Increases by value I (up to MAX) each time EFFECT is triggered
    // If current value + I = MAX, it returns 0.
    // If adding I exceeds MAX, the function returns 0 + any remainder in excesss of MAX 
    // I, MAX = numbers
    // return value: INTEGER

File: ./effect_position.h
// Usage: EffectPosition<>
    // Or: EffectPosition<EFFECT>
    // EFFECT: effect type
    // return value: INTEGER
    //
    // EffectPosition returns the position of a particular effect. 0 = base, 32768 = tip.
    // For now, this location is random, but may be set explicitly in the future.
    // When used as EffectPosition<> inside a TransitionEffectL whose EFFECT is already specified, 
    // then it will automatically use the right effect.

File: ./hold_peak.h
// Usage: HoldPeakF<F, HOLD_MILLIS, SPEED>
    // Holds Peak value of F for HOLD_MILLIS.
    // then transitions down over SPEED to current F
    // F, HOLD_MILLIS and SPEED: FUNCTION
    // return value: FUNCTION, same for all LEDs

File: ./ifon.h
// Usage: Ifon<A, B>
    // Returns A if saber is on, B otherwise.
    // A, B: INTEGER
    // return value: INTEGER
// Usage: InOutFunc<OUT_MILLIS, IN_MILLIS>
    // IN_MILLIS, OUT_MILLIS: a number
    // RETURN VALUE: FUNCTION
    // 0 when off, 32768 when on, takes OUT_MILLIS to go from 0 to 32768
    // takes IN_MILLIS to go from 32768 to 0.

File: ./increment.h
// Usage: IncrementModulo<PULSE, MAX, INCREMENT>
    // PULSE: FUNCTION (pulse type)
    // MAX: FUNCTION (not zero) defaults to Int<32768>
    // INCREMENT: FUNCTION defaults to Int<1>
    // Increments by I each time PULSE occurs wraps around when
    // it reaches MAX.
// Usage: ThresholdPulseF<F, THRESHOLD, HYST_PERCENT>
    // F: FUNCTION
    // THRESHOLD: FUNCTION (defaults to Int<32768>)
    // HYST_PERCENT: FUNCTION (defaults to Int<66>
    // Returns 32768 once when F > THRESHOLD, then waits until
    // F < THRESHOLD * HYST_PERCENT / 100 before going back
    // to the initial state (waiting for F > THRESHOLD).
// Usage: IncrementF<F, V, MAX, I, HYST_PERCENT>
    // Increases by value I (up to MAX) each time F >= V
    // Detection resets once F drops below V * HYST_PERCENT
    // if greater than MAX returns 0
    // F, V, I, MAX = numbers
    // HYST_PERCENT = percent (defaults to 66)
    // return value: INTEGER

File: ./int.h
// Usage: Int<N>
    // Returns N
    // N: a number
    // return value: INTEGER

File: ./int_arg.h

File: ./int_select.h
// Usage: IntSelect<SELECTION, Int1, Int2...>
    // SELECTION: FUNCTION
    // Returns SELECTION of N 
    // If SELECTION is 0, the first integer is returned, if SELECTION is 1, the second and so forth.
    // N: numbers
    // return value: INTEGER

File: ./isbetween.h
// Usage: IsBetween<F, BOTTOM, TOP>
    // Returns 0 or 32768 based F > BOTTOM and < TOP 
    // F, BOTTOM, TOP: INTEGER
    // return value: INTEGER

File: ./islessthan.h
// Usage: IsLessThan<F, V>
    // Returns 0 or 32768 based on V
    // If F < V returns 32768, if F >= V returns 0 
    // F, V: INTEGER
    // return value: INTEGER

File: ./layer_functions.h
// Usage: LayerFunctions<F1, F2, ...>
    // F1, F2: FUNCTIONS
    // return value: FUNCTION
    // Returns (32768 - (32768 - F1) * (32768 * F2) / 32768)
    // This is the same as 1-(1-F1)*(1-F2), but multiplied by 32768.
    // Basically Mix<LayerFunctions<F1, F2>, A, B> is the same as Mix<F2, Mix<F1, A, B>, B>.

File: ./linear_section.h
// Usage: LinearSectionF<POSITION, FRACTION>
    // POSITION: FUNCTION position on the blade, 0-32768
    // FRACTION: FUNCTION how much of the blade to light up, 0 = none
    // return value: FUNCTION
    // creates a "block" of pixels at POSITION taking up FRACTION of blade

File: ./marble.h
// Usage: MarbleF<OFFSET, FRICTION, ACCELERATION, GRAVITY>
    // OFFSET: FUNCTION  0-32768, adjust until "down" represents is actually down
    // FRICTION: FUNCTION, higher values makes the marble slow down, usually a constant
    // ACCELERATION: FUNCTION, a function specifying how much speed to add to the marble
    // GRAVITY: FUNCTION higher values makes the marble heavier
    // return value: FUNCTION  0-32768, representing point on a circle
    // This is intended for a small ring of neopixels.
    // It runs a simulation of a marble trapped in a circular
    // track and returns the position of that marble.
    // Meant to be used with CircularSectionF to turn the marble
    // position into a lighted up section.

File: ./mod.h
// Usage: ModF<F, MAX>
    // F: FUNCTION
    // MAX: FUNCTION (not zero)
    // When F is greater than MAX, F wraps to 0
    // When F is less than 0, F wraps to MAX
    // returns Integer

File: ./mult.h
// Usage: Mult<F, V>
    // Fixed point multiplication of values F * V, 
    // fixed point 16.15 arithmetic (32768 = 1.0)
    // (2*2 would not result in 4), 
    // (16384 * 16384 = 8192, representation of 0.5*0.5=0.25) 
    // most blade functions use this method of fixed point calculations
    // F, V: INTEGER, 
    // return value: INTEGER
// Usage: Percentage<F, V>
    // Gets Percentage V of value F, 
    // Percentages over 100% are allowed and will effectively be a multiplier. 
    // F, V: INTEGER
    // example Percentage<Int<16384>,25>
    // this will give you 25% of Int<16384> and returns Int<4096>
    // return value: INTEGER

File: ./on_spark.h
// Usage: OnsparkF<MILLIS>
    // MILLIS: FUNCTION (defaults to Int<200>)
    // return value: FUNCTION
    // When the blade turns on, this function starts returning
    // 32768, then fades back to zero over MILLIS milliseconds.
    // This is intended to be used with Mix<> or AlphaL<> to
    // to create a flash of color or white when the blade ignites.

File: ./ramp.h
// Usage: Remap<RampF,COLOR>
    // Returns led as value between 0 ~ 32768
    // Keeps existing mapping for pixels when used with Remap<>

File: ./random.h
// Usage: RandomF
    // Return value: FUNCTION
    // Returns a random number between 0 and 32768.
    // All LEDS gets the same value.
// Usage: RandomPerLEDF
    // Return value: FUNCTION
    // Returns a random number between 0 and 32768.
    // Each LED gets a different random value.
// Usage: EffectRandomF<EFFECT>
    // Returns a random value between 0 and 32768 each time EVENT is triggered
    // return value: INTEGER

File: ./random_blink.h
// Usage: RandomBlinkF<MILLIHZ>
    // MILLHZ: FUNCTION
    // Randomly returns either 0 or 32768 for each LED. The returned value
    // is held, but changed to a new random value MILLIHZ * 1000 times per
    // second.

File: ./readpin.h
// Usage: ReadPinF<PIN>
    // or: ReadPinF<PIN, PIN_MODE>
    // returns INTEGER, 0 if pin is low and 32768 if pin is high
    // PIN: int, pin you want your style to respond to
    // PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT
// Usage: AnalogReadPinF<PIN>
    // or: AnalogReadPinF<PIN, PIN_MODE>
    // returns INTEGER, 0-32768 depending on input reading.
    // PIN: int, pin you want your style to respond to
    // PIN_MODE: int, one of INPUT, INPUT_PULLUP or INPUT_PULLDOWN, defaults to INPUT
    // Notes:
    //   * May cause slowdowns
    //   * may not update every run() call
    //   * pin modes other than INPUT may not be supported,
    //   * Only analog-capable pins will work.

File: ./scale.h
// Usage: Scale<F, A, B>
    // Changes values in range 0 - 32768 to A-B
    // F, A, B: INTEGER
    // return value: INTEGER

File: ./sequence.h
// usage: SequenceF<millis_per_bits, bits, 0b0000000000000000, ....>
    // millis_per_bit: a number, millseconds spent on each bit
    // bits: a number, number of bits before we loop around to the beginning
    // 0b0000000000000000: 16-bit binary numbers containing the actual sequence.
    //
    // Returns 32768 if the current bit in the sequence is 1, 0 otherwise.
    // The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.
    // Note that if not all bits are used within the 16-bit number.
    // Example, an SOS pattern:
    // SequenceF<100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>

File: ./sin.h
// Usage: Sin<RPM, LOW, HIGH>
    // pulses between LOW - HIGH RPM times per minute
    // LOW: INTEGER (defaults to Int<0>)
    // HIGH: INTEGER (defaults to Int<32768>)
    // RPM: INTEGER
    // return value: INTEGER

File: ./slice.h
// Usage: SliceF<DENSITY_FUNCTION>
    // or: SliceF<DENSITY_FUNCTION, OFFSET>
    // DENSITY_FUNCTION: 3DF 
    // OFFSET: integer, defaults to 20
    // return value: FUNCTION
    // The DENSITY_FUNCTION is a 3-dimensional function, f(x, y, z)
    // the SliceF function calculates the x/y/z coordinates based on the
    // angle of the blade. For now, the only density functions available
    // are SmokeDF and FastSmokeDF, which are basically the same thing.
    // This is very similar to how the POV blade works, but instead of
    // using a large data blob as input, it just uses another function
    // as input.

File: ./smoothstep.h
// Usage: SmoothStep<POS, WIDTH>
    // POS, WIDTH: FUNCTION
    // return value: FUNCTION
    // POS: specifies the middle of the smoothstep, 0 = base of blade, 32768=tip
    // WIDTH: witdth of transition, 0 = no transition, 32768 = length of blade
    // Example: SmoothStep<Int<16384>, Int<16384>> returns 0 up until 25% of the blade.
    // From there it has a smooth transition to 32768, which will be reached at 75% of
    // the blade. If WIDTH is negative, the transition will go the other way.

File: ./sound_level.h
// Usage: SmoothSoundLevel
    // Returns 0-32768 based on sound level.
    // returned value: INTEGER
// Usage: NoisySoundLevel
    // Returns 0-32768 based on sound level.
    // returned value: INTEGER
// Usage: NoisySoundLevelCompat
    // Returns 0-32768 based on sound level.
    // This function is now used to implement the
    // AudioFlicker<> style, don't change it.
    // returned value: INTEGER

File: ./sparkle.h
// Usage: SparkleF<SPARK_CHANCE_PROMILLE, SPARK_INTENSITY>
    // SPARK_CHANCE_PROMILLE: a number
    // SPARK_INTENSITY: a number

File: ./strobe.h
// Usage: StrobeF<STROBE_FREQUENCY, STROBE_MILLIS>
    // STROBE_FREQUENCY_FUNC, STROBE_MILLIS_FUNC: FUNCTION
    // return value: INTEGER
    // Stroboscope-like effect, turns the color to STROBE_COLOR for STROBE_MILLIS
    // STROBE_FREQUENCY times per second.

File: ./subtract.h
// Usage: Subtract<A, B>
    // Subtracts B from A (A - B)
    // A, B: FUNCTION
    // return value: FUNCTION

File: ./sum.h
// Usage: SUM<A, B, ...>
    // Adds A + B...
    // A, B: INTEGER
    // return value: INTEGER

File: ./svf.h

File: ./swing_speed.h
// Usage: SwingSpeed<MAX>
    // Returns 0-32768 based on swing speed
    // returned value: INTEGER
// Usage: SwingAcceleration<MAX>
    // Returns 0-32768 based on swing acceleration
    // MAX defaults to 150
    // returned value: INTEGER

File: ./time_since_effect.h
// Usage: TimeSinceEffect<>
    // Or: TimeSinceEffect<EFFECT>
    // EFFECT: effect type
    // return value: INTEGER
    //
    // TimeSinceEffect returns the number of milliseconds since a particular
    // effect occured.
    // When used as TimeSinceEffect<> inside a TransitionEffectL whose EFFECT is already specified, 
    // then it will automatically use the right effect.

File: ./trigger.h
// Usage: Trigger<EFFECT, FADE_IN_MILLIS, SUSTAIN_MILLIS, FADE_OUT_MILLIS, DELAY>
    // Normally returns 0, but when EFFECT occurs, it ramps up to 32768,
    // stays there for SUSTAIN_MILLIS, then fades down to zero again.
    // If delay is specified, the whole thing is delayed that much before it starts.
    // EFFECT: BladeEffectType
    // FADE_IN_MILLIS: INTEGER
    // SUSTAIN_MILLIS: INTEGER
    // FADE_OUT_MILLIS: INTEGER
    // DELAY_MILLIS: INTEGER (defaults to Int<0>)
    // return value: INTEGER

File: ./twist_angle.h
// Usage: TwistAngle<N, OFFSET>
    // Returns 0-32768 based on angle of twist
    // OFFSET: Adjustable offset (0-32768) to make the twistangle values line up with how you hold the hilt.
    // N : Number of times the values goes from 0 to 32768 and back per hilt revolution.
    // returned value: FUNCTION, same for all leds
// Usage: TwistAcceleration<MAX>
    // Returns 0-32768 based on acceleration of twist in one direction
    // MAX : Maximum acceleration needed to return 32768
    // returned value: FUNCTION, same for all leds

File: ./variation.h
// Usage: Variation
    // Returns 0-32768 based on current variation.
    // returned value: FUNCTION
    // Note that using Variation in your style means that the
    // the automatic color rotation is turned off. The color wheel
    // menu is unaffected, but the style is now responsible for actually
    // changing the color.
    // Note that if any blade styles are using ColorChange<>,
    // the variation will return "ticked" values: 0, 1, 2, etc.

File: ./volume_level.h
// Usage: VolumeLevel
    // Returns 0-32768 based on volume level.
    // returned value: INTEGER

File: ./wavlen.h
// Usage: WavLen<>
    // Or: WavLen<EFFECT>
    // EFFECT: effect type
    // return value: INTEGER
    //
    // WavLen (length of wav file) takes the duration of a wav file sound
    // and can be used to replace time integer arguments in a blade style.
    // Example: TrFadeX<WavLen<EFFECT_RETRACTION>>
    // When used as WavLen<> inside a TransitionEffectL whose EFFECT is already specified, 
    // then it will automatically use the right effect.
    // Example: TransitionEffectL<TrConcat<TrWipex<WavLen<>>,White,TrWipeX<WavLen<>>>,EFFECT_BLAST>

File: ./wavnum.h
// Usage: WavNum<>
    // Or: WavNum<EFFECT>
    // EFFECT: effect type
    // return value: INTEGER
    //
    // Returns which file was actually played.
    // First file returns 0. Even if the file is called 'clash1.wav'.

```

