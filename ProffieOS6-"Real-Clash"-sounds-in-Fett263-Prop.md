In ProffieOS6, using Fett263's prop file you can enable clash, begin lockup and end lockup sounds to be selected based on the actual clash strength.

To enable use /props/saber_fett263_buttons.h

Your config should include the following define(s)

> ``#define FETT263_CLASH_STRENGTH_SOUND // enables Clash Strength selection for sounds``

> ``#define FETT263_MAX_CLASH 16 // optional define to set the hardest clash on saber range 8 ~ 16, defaults to 16 if not defined``

Then in your fonts you will set up your clsh.wav, bgnlock.wav and endlock.wav (if more than one file) sequentially with the sounds for the lightest clashes as the lowest file numbers and the hardest clashes as the highest numbers.

Example (files must be numbered sequentially you cannot skip a number or you will get "error in font directory"):
* clsh01.wav = lightest clash sound
* clsh02.wav
* clsh03.wav
* ...
* clsh16.wav

You can combine the sounds with Clash and Lockup Effects that utilize the ClashImpactF<> function to create "Real Clash" effects that match the sound and effect to the actual strength of the clash.