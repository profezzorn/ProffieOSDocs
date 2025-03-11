# Array Selector Explained

## Principles and Practice
Array selection is a seemingly simple tool that is actually surprisingly powerful. The idea is that multiple different blade settings can be accessed at the press of a button, with simple config tweaks providing enormous options. Adjustments to the blade array can help build many different Array Selection setups, such as:

- By specifying dummy blades, you can have a different number of effective blades on the same saber by switching arrays.
- Multiple blade arrays can all look at the same preset array.
- Specifying or not specifying individual save files per blade array allows you to control which blade preset (font) you land on when you switch into a new array.
- If you have the same number of presets in multiple preset arrays, array switching can become invisible and appear to the user as a simple toggle between single differences between preset arrays.

To add array selection to your saber, you need to add the following define to the CONFIG_TOP section of your config:

`#define SABERSENSE_ARRAY_SELECTOR`

When switching arrays, the switch is confirmed by playing an associated arrayx.wav file. If no array file is available, the system will play the font.wav file instead.
A further optional define will play the arrayx.wav file *and* the font.wav file:

`#define SABERSENSE_ENABLE_ARRAY_FONT_IDENT`

This helps when you have arrays set to save the last font used in that array, as it tells you which font you've landed on when you perform an array switch.

## Array Saving

By default, the system will save which array you're on. This means that the system will boot up into the last array that you were using.
You can disable array saving by adding this define to the CONFIG_TOP section of your config:

`#define SABERSENSE_DISABLE_SAVE_ARRAY`

## Specifying Arrays

You will also need to specify the arrays themselves, with sequential index numbers starting at zero, like this:

```
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

```
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

# Example Implementations
To illustrate the above concepts, let's look at some examples of how they might be implemented:

## Different Blade Lengths
- Array 1 - KR 36 inch
- Array 2 - LGT 35 inch
- Array 3 - KR 33 inch
- Array 4 - LGT 32 inch
- Array 5 - Unspecified 144 pixels

This can be achieved by having unspecified save files and all blade arrays looking at the same preset array - all that changes is the pixel count between blade arrays. This means to the end user, switching arrays simply changes the blade length setting without affecting anything else.

## Turning Motors On and Off
- Array 1 - Motor On when blade lights
- Array 2 - Motor Off 

Things like this can be done one of two ways...
Either have a single preset array with two blade arrays, and on the second blade array (motor off) specify an unused LED power pad for the motor. This way the motor never receives the preset instruction to start up.
Alternatively have two preset arrays, both idential except for the motor preset which is set for off.
If you opt for the latter, you can also specifiy two separate save files in the blade array. This means when you switch into the opposite array, you will land on the blade preset (font) that was last used on that array.
Conversely, if you don't specify any save files, and you're on preset number six on array one for example, you will land on preset six again when you switch to array two.


## Adding Different Effects Options
- Array 1 - Light blade flicker, crystal follows blade
- Array 2 - Light blade flicker, crystal pulses when off
- Array 3 - Heavy blade flicker, crystal follows blade
- Array 4 - Heavy blade flicker, crystal pulses when off

By having four preset arrays, all listing the same fonts, you can simply add different blade styles to each one. As above, not specifying save files means array switching doesn't affect which font you're on. Or you can specifiy save files and each array will remember the last font associated with that array and skip to that font the next time you switch back to that array.

## Having Emitter Animations on Multi-Pixel Blade Connectors
- Array 1 - Emitter animations
- Array 2 - Normal blade function 

By using dummy blades, we can split 16 pixel Shtok connectors into two blades for blade out settings, giving greater scope for different emitter animations, while keeping normal blade functionality when using a blade.

## Split Presets/Fonts Into Groups
- Array 1 - Light Side Fonts
- Array 2 - Dark Side Fonts
- Array 3 - Unstable Fonts
- Array 4 - Blade Plug Charging Mode

Simply lay your blade presets out as per above, and point the four identical blade arrays to each preset array respectively.

## Provide 'User Favourite' Functionality
- Array 1 - User Favourite 1
- Array 2 - User Favourite 2
- Array 3 - User Favourite 3
- Array 4 - User Favourite 4
- Array 5 - User Favourite 5
- Array 6 - User Favourite 6

On sabers with very large number of sound fonts, this feature allows users to have them all available but to select (in the case above) six easily-accessible favourites.
To make it work, simply specify unique save files to each blade array and the system will always remember, and return to, the font that was last used on a given array when you switch to it.
If you add the define to play the font ident after each array switch, it will tell you which font you've landed on when you switch arrays. Or alternatively, simply delete the arrayx.wav files from the SD card, and the system will play the font idents instead of the array idents automatically.

## Power Saving Mode
- Array 1 - Full Power Mode
- Array 2 - Half Power Mode

Point both blade arrays at the same preset array and set one array with `{ 0, DimBlade(50.0, WS281XBladePtr etc.`, and array switching becomes a way of entering and exiting a low power battery saving mode. For even more clarity, make array1.wav say, *"Exiting low power mode"* and make array2.wav say, *"Entering Low power Mode"*, and user navigation becomes even slicker. (A range of various idents are available from the Sabersense website - simply rename the files you need appropriately.

## Mix Blade Length and User Favourites
- Array 1 - KR 36 inch, User save font 1
- Array 2 - KR 36 inch, User save font 2
- Array 3 - KR 36 inch, User save font 3
- Array 4 - KR 32 inch, User save font 1
- Array 5 - KR 32 inch, User save font 2
- Array 6 - KR 32 inch, User save font 3

A single preset array, individual specified save files, gives the option to save three favourite fonts per blade length.

## Always a Way Out...
If users end up with arrays saved in ways they don't want, all they need do is *four-clicks-and-hold* the Power button and the system will completely reset to config defaults by deleting all the save files.
