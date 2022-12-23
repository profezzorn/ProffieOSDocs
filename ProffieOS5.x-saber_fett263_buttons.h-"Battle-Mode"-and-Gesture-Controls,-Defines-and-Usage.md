# Fett263 Prop File with "Battle Mode" and Gesture Controls for ProffieOS5.x

Instructions for including in your config at bottom of the page.

## New features: 

- "Battle Mode" - gesture controlled Lockup, Melt, Drag 

- "Force Push" - a new gesture during Battle Mode, pushing your hilt towards you opponent quickly will trigger a force push sound (push.wav or force.wav) (this is optional with a define)

- Gesture Ignitions and Retractions - Swing On, Stab On, Thrust On and Twist On with Twist Off

- "Fast On" for Gesture Ignitions - ignored preon.wav and Preon effects and just ignites the blade on a gesture movement. By default all Gesture Ignitions will use Fast On and ignore Preon sounds and effects (this is customizable with defines if you want to enable Preons with Gestures)

- On Demand "Power Save" and "Battery Level" effects - enable a dimming effect on your presets (via styles) to dim the blade brightness and save power on demand and view your current Battery Level with a custom style with a button press.

- Multi-Phase - change presets while the blade is ignited

- Multi-Blast Mode (from OS4.8 but can be used with Battle Mode) - activate to enable a blast effect for every blade swing/deflection

- New Mode, Menu and Feature sound effects (add these new sounds to your font/preset for additional customization)

> *    On Demand Power Save - dim.wav

> *    On Demand Battery Level - battery.wav

> *    Battle Mode On (on toggle) - bmbegin.wav

> *    Battle Mode Off (on toggle) - bmend.wav

> *    Enter Volume Menu - vmbegin.wav

> *    Exit Volume Menu - vmend.wav

> *    Fast On (optional) - faston.wav

> *    Multi-Blast Mode On - blstbgn.wav

> *    Multi-Blast Mode Off - blstend.wav

## While in Battle Mode - Lockup, Drag and Melt are all controlled by gestures only, no buttons are needed:

- Lockup is initiated with a clash, if you hold your saber against your opponent's (or keep relatively still) Lockup will be active, to disengage Lockup you will pull your saber away from the opponents. During Lockup you can move your saber against your opponents and the Responsive effects will still respond to blade angle as you "struggle" the "pull away" motion is a deliberate change in angle (this can take a little practice).

- Clash in "Battle Mode" is actually Begin Lockup/End Lockup in quick succession based on clashing your saber and pulling away immediately. As a result, your style needs to include LOCKUP_BEGIN and LOCKUP_END transitions, the combination of these transitions will create your "clash" effect. I have updated my library to now allow you to choose several options for both the begin and end Lockup in the Enhancement screen. You can mix and match as you like although some combinations work better together than others so test and decide for yourself. NOTE: bgnlock.wav and endlock.wav will be used, in testing you can rename your clsh.wav sounds to bgnlock.wav to your preference, some work better than others so it's ultimately up to the user. While in Battle Mode your actual Clash effects and Sounds are not used. I have timed out the Begin and End transitions on the library but you can customize to shorten or lengthen the visual effect, there is also a control factor in that if you don't pull away immediately the actual Lockup effect will appear so learning to control the saber is a part of the effect.
- NOTE: OS 5.7 added an update for swinging through the clash.  If you have a glancing clash or continue a swing after a clash your saber will do a traditional clash, if your blade comes to a stop or slows down it will go into Begin Lockup/End Lockup.

- There is a new threshold for use with the Battle Mode features, it mostly affects "Lockup/Clash" as when you normally clash two sabers together there is a "bounce" that happens, the threshold wil let you ignore the "bounce" so Lockup can properly engage but if you have it too high then "clash" is harder to perform. I have defaulted to the "Goldilocks" zone I found in testing. If you wish to change you will use:

>>  #define FETT263_LOCKUP_DELAY 200 

>> (200 is the default, increasing will allow for more time to determine Lockup, decreasing will shorten)

> > This works in conjunction with the CLASH_THRESHOLD_G define, CLASH_THRESHOLD_G is the level to recognize the clash/stab event occured if the effects trigger too easily you will increase this value, if they are not triggering easily you will lower this value. After the Clash occurs the LOCKUP_THRESHOLD is used as noted above. The combination of these two thresholds is then used with your control of the saber for "pulling away" and the styles in your preset to create Clash/Lockup.

- Drag in "Battle Mode" is activated by Stabbing down, this is to allow you to clash and lockup with your blades below horizontal like in the films. The Stab motion is a linear thrust down with contact (or an abrupt end). While Drag is active you can "drag" it along the floor to intimidate your opponent. To disengage Drag you only need to lift the blade from the floor at an angle. Drag (and Melt) have a lower threshold than Lockup so you won't need as deliberate a movement to "pull away".

- Melt in "Battle Mode" is activated by stabbing horizontal or up, you can use the Responsive Melt to heat up the surface by turning your hilt and you can drag your saber along the wall/object, to disengage Melt you will pull away from the wall or object at an angle.

NOTE: Stab is not active during Battle Mode, if you do a quick Melt/Drag and pull away you can get a quasi-Stab effect. To use Stab (particularly for the new Summon and Release effects) you will exit "Battle Mode" by holding Aux and Swinging.

## DEFAULT 2 BUTTON CONTROLS (PWR and AUX):

* "Battle Mode" - hold AUX and Swing while blade is ON to toggle mode ON/OFF

* Ignite (ON) - click PWR while OFF (Swing On, Twist On, Thrust On and Stab On available with defines)

* Muted Ignition (ON) - double click PWR while OFF

* Retract (OFF) - click PWR while ON (disabled during swinging, Twist Off available with define)

* Play/Stop Music Track - hold and release PWR while OFF or hold and release PWR while pointing blade straight up while ON

* Blast - click AUX while ON

* Multi-Blast Mode - hold and release AUX while ON to enter mode, Swing to initiate Blasts, click Aux to exit mode (lockup, clash, stab, melt, drag or any button presses automatically exits mode)

* Clash - clash blade while ON, in Battle Mode clash and pull away quickly for "Clash" (requires BEGIN_LOCKUP and END_LOCKUP styles and sounds)

* Lockup - hold AUX and clash while ON, in Battle Mode clash and hold steady to activate, pull away to disengage

* Drag - hold AUX and stab down while ON, in Battle Mode stab down, pull away to disengage

* Melt - hold PWR (or AUX) and thrust forward and clash while ON	in Battle Mode thrust and clash to engage, pull away to disengage

* Lightning Block - hold PWR and click AUX while ON

* Force - hold and release PWR while ON (except while pointing blade straight up)

* Stab - thrust forward and clash blade while ON - deactivated in Battle Mode

* Power Save - hold Aux and click PWR while ON (pointing up) to use Power Save (requires style)

* Color Change - hold AUX and click PWR while ON (parallel or down) to enter CCWheel, turn hilt to rotate through colors, click PWR to select/exit if using COLOR_CHANGE_DIRECT each button press advances one Color at a time

* Next Preset - click AUX while OFF (parallel or up)

* Previous Preset - click Aux while OFF (pointing down)

* MULTI_PHASE Next Preset - hold AUX and TWIST while ON (use define to enable)

* MULTI_PHASE Previous Preset - hold PWR and TWIST while ON (use define to enable)

* Battery Level - hold AUX and click PWR while OFF (requires style)

* Enter SA22C Volume Menu - hold and release AUX while OFF

* Volume Up (10% increment, 100% max) - click PWR while in Volume Menu while OFF

* Volume Down (10% increment) - click AUX while in Volume Menu while OFF

* Exit Volume Menu - hold and release AUX while in Volume Menu while OFF

## OPTIONAL DEFINES (added to CONFIG_TOP in config.h file)

**#define FETT263_BATTLE_MODE_ALWAYS_ON**

Battle Mode is always on, toggle controls deactivated, This will disable traditional Clash and Stab effects, (cannot be used with #define FETT263_BATTLE_MODE_START_ON)

or


**#define FETT263_BATTLE_MODE_START_ON**

Battle Mode is active with each ignition by default but can be toggled using Aux + Swing control, (cannot be used with #define FETT263_BATTLE_MODE_ALWAYS_ON)


**#define FETT263_LOCKUP_DELAY 200**

This is the "delay" in millis to determine Clash vs Lockup


**#define FETT263_BM_DISABLE_OFF_BUTTON**

During Battle Mode Power Button Retraction is disabled


**#define FETT263_SWING_ON**

To enable Swing On Ignition control (automatically enters Battle Mode, uses Fast On)

or


**#define FETT263_SWING_ON_PREON**

Disables Fast On ignition for Swing On so Preon is used (cannot be used with #define FETT263_SWING_ON)


**#define FETT263_SWING_ON_NO_BM**

To enable Swing On Ignition control but not activate Battle Mode, (Combine with #define FETT263_SWING_ON or FETT263_SWING_ON_PREON to enable, cannot be used with #define FETT263_BATTLE_MODE_ALWAYS_ON or #define FETT263_BATTLE_MODE_START_ON)


**#define FETT263_SWING_ON_SPEED 250**

Adjust Swing Speed required for Ignition 250 ~ 500 recommended


**#define FETT263_TWIST_OFF**

To enable Twist Off Retraction control


**#define FETT263_TWIST_ON**

To enable Twist On Ignition control (automatically enters Battle Mode, uses Fast On)

or


**#define FETT263_TWIST_ON_PREON**

Disables Fast On ignition for Twist On so Preon is used (cannot be used with #define FETT263_TWIST_ON)


**#define FETT263_TWIST_ON_NO_BM**

To enable Twist On Ignition control but not activate Battle Mode, (Combine with #define FETT263_TWIST_ON or FETT263_TWIST_ON_PREON to enable, cannot be used with #define FETT263_BATTLE_MODE_ALWAYS_ON or #define FETT263_BATTLE_MODE_START_ON)


**#define FETT263_STAB_ON**

To enable Stab On Ignition control (automatically enters Battle Mode, uses Fast On)

or


**#define FETT263_STAB_ON_PREON**

Disables Fast On ignition for Stab On so Preon is used (cannot be used with #define FETT263_STAB_ON)


**#define FETT263_STAB_ON_NO_BM**

To enable Stab On Ignition control but not activate Battle Mode, (Combine with #define FETT263_STAB_ON or FETT263_STAB_ON_PREON, cannot be used with #define FETT263_BATTLE_MODE_ALWAYS_ON or #define FETT263_BATTLE_MODE_START_ON)


**#define FETT263_THRUST_ON**

To enable Thrust On Ignition control (automatically enters Battle Mode, uses Fast On)

or


**#define FETT263_THRUST_ON_PREON**

Disables Fast On ignition for Thrust On so Preon is used (cannot be used with #define FETT263_THRUST_ON)


**#define FETT263_THRUST_ON_NO_BM**

Combine with #define FETT263_THRUST_ON or FETT263_THRUST_ON_PREON, (cannot be used with #define FETT263_BATTLE_MODE_ALWAYS_ON or #define FETT263_BATTLE_MODE_START_ON)


**#define FETT263_FORCE_PUSH**

To enable gesture controlled Force Push during Battle Mode, (will use push.wav or force.wav if not present)


**#define FETT263_FORCE_PUSH_ALWAYS_ON**

To enable gesture controlled Force Push full time, (will use push.wav or force.wav if not present)


**#define FETT263_FORCE_PUSH_LENGTH 5**

Allows for adjustment to Push gesture length in millis needed to trigger Force Push
Recommended range 1 ~ 10, 1 = shortest, easiest to trigger, 10 = longest


**#define FETT263_MULTI_PHASE**

This will enable a preset change while ON to create a "Multi-Phase" saber effect


**#define MOTION_TIMEOUT 60 * 15 * 1000**

This extends the motion timeout to 15 minutes to allow gesture ignition to remain active, Increase/decrease the "15" value as needed


## Including prop file in config.h

To use this prop file you will include in your config and list the defines from above based on the controls and features you wish to enable. (see example below)

## Example config (top section):

***

#ifdef CONFIG_TOP

#include "proffieboard_v2_config.h"

#define NUM_BLADES 1

#define NUM_BUTTONS 2

#define VOLUME 1500

const unsigned int maxLedsPerStrip = 144;

#define CLASH_THRESHOLD_G 2.0

#define ENABLE_AUDIO

#define ENABLE_MOTION

#define ENABLE_WS2811

#define ENABLE_SD

#define COLOR_CHANGE_DIRECT

#define DISABLE_DIAGNOSTIC_COMMANDS

**#define FETT263_THRUST_ON** // enables Thrust On Ignition

**#define FETT263_SWING_ON** // enables Swing On Ignition

**#define FETT263_TWIST_ON** // enables Twist On Ignition

**#define FETT263_TWIST_OFF**  // enables Twist Off Retraction

**#define FETT263_FORCE_PUSH** // enables Force Push gesture/sound during Battle Mode

**#define MOTION_TIMEOUT 60 * 15 * 1000** // keeps motion chip active for 15 minutes while blade is Off

**#define FETT263_MULTI_PHASE** // enables Multi-Phase preset changing while blade is ON

#endif

**#ifdef CONFIG_PROP**

**#include "../props/saber_fett263_buttons.h"**

**#endif**

#ifdef CONFIG_PRESETS

Preset presets[] = {...


***

## GESTURE CONTROLS

[PDF Version](https://fett263.s3.us-east-2.amazonaws.com/fett263-proffieOS5-gesture-controls.pdf)

![Gesture Controls](https://fett263.s3.us-east-2.amazonaws.com/fett263-proffieOS5-gesture-controls.jpg)
