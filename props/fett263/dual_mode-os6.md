In ProffieOS6 using Fett263's prop file you can set your font up to select ignition, preon, retraction and postoff sounds based on blade position.  With the odd numbered files being used when the blade is pointing up and even numbered files being used when the blade is pointing down.

You will need to use /props/saber_fett263_buttons.h

And add this define to your config:

> `#define FETT263_DUAL_MODE_SOUND`

This will allow you to have different length sounds, dual ignition sounds for Crossguards or Staff sabers, or varied ignition, preon, retraction and postoff sounds within a font.

You will set your font up with the even sounds for when your saber is pointing down and odd sounds for when your saber is pointing up as long as there is more than one of each sound. The sounds will be randomly selected from odd or even files based on the blade orientation when effect is triggered.

Example:
* out01.wav //randomly selected when blade is up
* out02.wav //randomly selected when blade is down
* out03.wav //randomly selected when blade is up
* out04.wav //randomly selected when blade is down

In addition, you can set effects for Ignition, Preon and Retraction using BladeAngle<> to have unique effects for both positions (up or down) including setting up an effect for only one position if you desire.

You can also use WavLen<> function to set the timing of the effect based on the sound file used and have longer or shorter files used in the odd/even set up to have the effect match the sound based on blade orientation.