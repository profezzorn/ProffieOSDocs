---
title: Sabersense Array Selector
---

## Principles and Practice
Array selection is a seemingly simple tool that is actually surprisingly powerful. The Sabersense Array Selector utilizes the ProffieOS BladeID engine, replacing regular BladeID with the ability to cycle through blade arrays manually. The idea is that multiple different blade settings can be accessed at the press of a button, with simple config tweaks providing enormous options. Adjustments to the blade array can help build many different Array Selection setups, such as:

* By specifying dummy blades, you can have a different number of effective blades on the same saber by switching arrays.
* Multiple blade arrays can all look at the same preset array.
* Specifying or not specifying individual save files per blade array allows you to control which blade preset (font) you land on when you switch into a new array.
* If you have the same number of presets in multiple preset arrays, array switching can become invisible and appear to the user as a simple toggle between single differences between preset arrays.

To add array selection to your saber, you need to add the following define to the CONFIG_TOP section of your config:

`#define SABERSENSE_ARRAY_SELECTOR`

Arrays must be numbered sequentially, starting at zero (0), in the field that would otherwise contain BladeID values. If using Array Selector with Blade Detect, you must add `#define SABERSENSE_NO_BLADE` to the top of your config. You also need to replace the zero (0) in the first array with NO_BLADE. When the end user cycles through the arrays, the NO_BLADE array will be ignored by Array Selector and will only be accessed by the Blade Detect process. Further details about Blade Detect can found here: https://pod.hubbe.net/howto/blade-detect.html

When switching arrays, the switch is confirmed by playing an associated arrayx.wav file. If no array file is available, the system will play the font.wav file instead. A further optional define will play the arrayx.wav file *and* the font.wav file:

`#define SABERSENSE_ENABLE_ARRAY_FONT_IDENT`

This helps when you have arrays set to save the last font used in that array, as it tells you which font you've landed on when you perform an array switch.

## Array Saving

By default, the system will save which array you're on. This means that the system will boot up into the last array that you were using. You can disable array saving by adding this define to the CONFIG_TOP section of your config:

`#define SABERSENSE_DISABLE_SAVE_ARRAY`

## Default Array
In multi-array systems, you can specify which array should be the default by adding this define to the CONFIG_TOP section of your config file, followed by the index number of the array you want (note zero based numbering):

`#define SABERSENSE_DEFAULT_BLADE_ARRAY 4`

## Specifying Arrays

You will also need to specify the arrays themselves, with sequential index numbers starting at zero, like this:

```cpp
BladeConfig blades[] = {
    { 0,
      //  Main Blade:
      WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets),  "Save1"}
    { 1,
       //  Main Blade:
       WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
       //  Crystal Chamber:   
       WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
       CONFIGARRAY(presets),  "Save2"}
    { 2,
      //  Main Blade:
      WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets),  "Save3"}
    { 3,
      //  Main Blade:
      WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets),  "Save4"}
  };
#endif
```

In the above example, all arrays are identical, all are looking at the same presets array (presets) but all have separate save folders specified (Save1, Save2 etc.). This means that when you switch from one array to another, the system will remember which font you were on on the previous array and will switch to that font when you next cycle to that array.

Note that the save references pertain to folders that the system will store the save files in. This means in the above instance, you would need to create the four save folders on the SD card yourself - the system will then place the save files inside those folders.

An alternative implementation might look like this:

```cpp
BladeConfig blades[] = {
    { 0,
      //  Main Blade:
      WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    { 1,
      //  Main Blade:
      WS281XBladePtr<122, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    { 2,
      //  Main Blade:
      WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    { 3,
      //  Main Blade:
      WS281XBladePtr<98, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    };
#endif
```
In this instance, the only difference is the pixel count. This means switching array will stay on the same font that you're currently on, but all that will change is the blade length.

## Using with Blade Detect

If using with blade detect, you must change the name of the first array from zero (0) to NO_BLADE, like this:
```cpp
BladeConfig blades[] = {
    { NO_BLADE,
      //  Main Blade:
      WS281XBladePtr<16, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(no_blade)},
    { 1,  // KR 36 inch blade.
      //  Main Blade:
      WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    { 2,  // KR 32 inch blade.
      //  Main Blade:
      WS281XBladePtr<122, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    { 3,  // KR Shoto blade.
      //  Main Blade:
      WS281XBladePtr<108, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3>>(),
      //  Crystal Chamber:   
      WS281XBladePtr<1, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin4>>(),  
      CONFIGARRAY(presets)},
    };
#endif
```
With this setup, the system will switch to the NO_BLADE array only when told to do so by the Blade Detection pin. By contrast, the manual Array Selector will ignore the NO_BLADE array and only cycle through the numbered arrays.

# Example Implementations
To illustrate the above concepts, let's look at some examples of how they might be implemented:

## Different Blade Lengths
* Array 1 - KR 36 inch
* Array 2 - LGT 35 inch
* Array 3 - KR 33 inch
* Array 4 - LGT 32 inch
* Array 5 - Unspecified 144 pixels

This can be achieved by having unspecified save files and all blade arrays looking at the same preset array - all that changes is the pixel count between blade arrays. This means to the end user, switching arrays simply changes the blade length setting without affecting anything else, and the system will save the stored length through reboots. You can then use the free wav file downloads available from the [Sabersense Downloads](https://www.sabersense.co.uk/downloads) page to ident which blade length you've switched to.

## Turning Motors On and Off
* Array 1 - Motor On when blade lights
* Array 2 - Motor Off 

Things like this can be done one of two ways...

Either have a single preset array with two blade arrays, and on the second blade array (motor off) specify an unused LED power pad for the motor. This way the motor never receives the preset instruction to start up.

Alternatively have two preset arrays, both idential except for the motor preset which is set for off.

If you opt for the latter, you can also specifiy two separate save files in the blade array. This means when you switch into the opposite array, you will land on the blade preset (font) that was last used on that array. Conversely, if you don't specify any save files, and you're on preset number six on array one for example, you will land on preset six again when you switch to array two.

## Adding Different Effects Options
* Array 1 - Light blade flicker, crystal follows blade
* Array 2 - Light blade flicker, crystal pulses when off
* Array 3 - Heavy blade flicker, crystal follows blade
* Array 4 - Heavy blade flicker, crystal pulses when off

By having four preset arrays, all listing the same fonts, you can simply add different blade styles to each one. As above, not specifying save files means array switching doesn't affect which font you're on. Or you can specifiy save files and each array will remember the last font associated with that array and skip to that font the next time you switch back to that array.

## Having Emitter Animations on Multi-Pixel Blade Connectors
* Array 1 - Emitter animations
* Array 2 - Normal blade function 

By using dummy blades, we can split 16 pixel Shtok connectors into two blades for blade out settings, giving greater scope for different emitter animations, while keeping normal blade functionality when using a blade.

## Split Presets/Fonts Into Groups
* Array 1 - Light Side Fonts
* Array 2 - Dark Side Fonts
* Array 3 - Unstable Fonts
* Array 4 - Blade Plug Charging Mode

Simply lay your blade presets out as per above, and point the four identical blade arrays to each preset array respectively.

## Provide 'User Favourite' Functionality
* Array 1 - User Favourite 1
* Array 2 - User Favourite 2
* Array 3 - User Favourite 3
* Array 4 - User Favourite 4
* Array 5 - User Favourite 5
* Array 6 - User Favourite 6

On sabers with very large number of sound fonts, this feature allows users to have them all available but to select (in the case above) six easily-accessible favourites. To make it work, simply specify unique save files to each blade array and the system will always remember, and return to, the font that was last used on a given array when you switch to it.

If you add the define to play the font ident after each array switch, it will tell you which font you've landed on when you switch arrays. Or alternatively, simply delete the arrayx.wav files from the SD card, and the system will play the font idents instead of the array idents automatically.

## Power Saving Mode
* Array 1 - Full Power Mode
* Array 2 - Half Power Mode

Point both blade arrays at the same preset array and set one array with `{ 0, DimBlade(50.0, WS281XBladePtr etc.`, and array switching becomes a way of entering and exiting a low power battery saving mode. For even more clarity, make array1.wav say, *"Exiting low power mode"* and make array2.wav say, *"Entering Low power Mode"*, and user navigation becomes even slicker. (A range of various idents are available from the Sabersense website - simply rename the files you need appropriately.

## Mix Blade Length and User Favourites
* Array 1 - KR 36 inch, User save font 1
* Array 2 - KR 36 inch, User save font 2
* Array 3 - KR 36 inch, User save font 3
* Array 4 - KR 32 inch, User save font 1
* Array 5 - KR 32 inch, User save font 2
* Array 6 - KR 32 inch, User save font 3

A single preset array, individual specified save files, gives the option to save three favourite fonts per blade length.

## Switch Audio Players On and Off
* Array 1 - Includes Force/Quote/Track Players
* Array 2 - Disables Force/Quote/Track Players

If we duplicate our preset array but make small changes to the folder and file paths and a couple of audio files for each preset, the Array Selector can become a toggle to switch effects player functionality on and off.

For example the top line of a preset might look like this:
```cpp
  {"DarkLord;common", "tracks/Imperial_March.wav",
```

In this instance, 'DarkLord' is the name of the font folder, followed by 'common', which typically houses files shared by all presets, and the music track is the *Imperial_March.wav* file inside the 'tracks' folder. When the system needs a file, it will look first in the 'DarkLord' folder, and if it can't find the file it needs there, it will then look inside 'common'. And when you play a track, it will access and play the *Imperial_March.wav* file.

If we duplicate the complete presets array but add a 'PreFont' folder and *Mute.wav* music track to each preset on one of the arrays like this:
```cpp
  {"PreFont;DarkLord;common", "tracks/Mute.wav",
```
then the system will look first in the 'PreFont' folder for any effects it wants. If it's looking for *quote* or *force* - and 'PreFont' contains *quote.wav* and *force.wav* files, both comprising one second of silence - the system will play those silent files and not look any further. The same goes for adding a *mute.wav* file to the 'tracks' folder.

As long as both preset arrays are otherwise the same and we don't specify separate save file locations for each one, the Array Selector will, to the end user, simply become a toggle to switch effect player functionality on or off.

## Always a Way Out...
If users end up with arrays saved in ways they don't want, all they need do is *four-clicks-and-hold* the Power button and the system will completely reset to config defaults by deleting all the save files. More details can be found here: https://pod.hubbe.net/props/sabersense/restore_defaults
