---
title: "Responsive Styles & Effects for ProffieOS 4.x or later."
redirect_from:
  - "/responsive-styles-&-effects.html"
---
Responsive Styles use BladeAngle<> or TwistAngle<> functions to control, modify or move effects in real-time, they are implemented using the below styles. The Responsive Styles all use Layers<> for implementation.

Defaults are included to make implementation as easy as adding just the COLOR or you can customize using the other parameters in the styles.

Example:
 
> `StylePtr<InOutHelper<Layers<`
`BASE, `
`ResponsiveClashL< COLOR >, `
`ResponsiveBlastL< COLOR >, `
`ResponsiveStabL< COLOR >, `
`ResponsiveLockupL< COLOR >, `
`ResponsiveDragL< COLOR >, `
`ResponsiveLightningBlockL< COLOR >, `
`ResponsiveMeltL< > >, `
`OUT_MILLIS, IN_MILLIS, OFF_COLOR>>()`

Responsive Styles can also be mixed with Standard styles, you do not need to use only Responsive styles, however, you probably only want one version of any effect otherwise Layer order will control which shows or both may show and conflict if one is partial blade and one is full blade.

Templates (only COLOR is required to implement - all values are defaulted for simple implementation) *except for ResponsiveMeltL<> which defaults all parameters to allow responsive Melt effect:

### ResponsiveLockupL<LOCKUP COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>
Implements LocalizedLockup that will move based on the angle of the blade
* TRANSITION1 & TRANSITION2 = transition Begin & End
* TOP = uppermost lockup position limit, BOTTOM = lowermost lockup position limit, Int<32768> = tip, Int<0> = hilt
* SIZE controls LOCKUP area size Int<0> ~ Int<32768>

### ResponsiveDragL<DRAG COLOR, TRANSTION1, TRANSITION2, SIZE1, SIZE2>
Implements Drag that will increase or decrease in size based on turning hilt
* TRANSITION1 & TRANSITION2 = transition Begin & End
* SIZE1 & SIZE2 control limits for DRAG size with TwistAngle

### ResponsiveMeltL<MELT COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>
Implements Melt effect for cutting through object, color will change to mimic metal heating* and intensity will increase or decrease based on turning hilt. 
*This requires the MELT COLOR enable TwistAngle<>, static COLORS or EFFECTS will not perform this effect. In the OS all of the parameters are defaulted so ResponsiveMeltL can be implemented as a Layer with no input as ResponsiveMeltL<>
* TRANSITION1 & TRANSITION2 = transition Begin & End
* SIZE1 & SIZE2 control MELT area limits for TwistAngle<>

### ResponsiveLightningBlockL<LIGHTNING BLOCK COLOR, TRANSITION1, TRANSITION2>
Implements hybrid Force Lightning Block with animation, intensity responds to turning the hilt and location/focus will respond to blade angle
* TRANSITION1 & TRANSITION2 = transition Begin & End

### ResponsiveClashL<CLASH COLOR, TRANSITION1, TRANSITION2, TOP, BOTTOM, SIZE>
Implements LocalizedClash effect that mimics ResponsiveLockup location and size (unless changed by user)
* TRANSITION1 & TRANSITION2 = transition Begin & End
* TOP = uppermost Clash position limit, BOTTOM = lowermost Clash position limit, Int<32768> = tip, Int<0> = hilt
* SIZE controls Clash area size Int<0> ~ Int<32768>

### ResponsiveBlastL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and disperse along the blade from original position
* FADE = fade time ms
* WAVE_SIZE = size
* WAVE MS = speed ms
* TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, Int<32768> = tip, Int<0> = hilt
* EFFECT = effect type, defaults to EFFECT_BLAST

### ResponsiveBlastWaveL<BLAST COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_SPEED, TOP, BOTTOM, EFFECT>
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and split up and down the length of the blade from original position
* FADE = fade time ms
* WAVE_SIZE = size
* WAVE MS = speed ms
* TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, Int<32768> = tip, Int<0> = hilt
* EFFECT = effect type, defaults to EFFECT_BLAST

### ResponsiveBlastFadeL<BLAST COLOR, SIZE, FADE, TOP, BOTTOM, EFFECT>
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and Fade in position
* SIZE controls blast size bump 0 ~ 32768
* FADE = fade time ms
* TOP = uppermost Blast position limit, BOTTOM = lowermost Blast position limit, Int<32768> = tip, Int<0> = hilt
* EFFECT = effect type, defaults to EFFECT_BLAST

### ResponsiveStabL<STAB COLOR, TRANSITION1, TRANSITION2, SIZE1, SIZE2>
Stab effect
Implements Stab effect that will change in size based on angle of the blade
* TRANSITION1 & TRANSITION2 = transition Begin & End
* SIZE1 & SIZE2 control Stab area limits for BladeAngle, Int<0> ~ Int<32768>
