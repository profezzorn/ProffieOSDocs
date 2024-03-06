---
title: How many leds does my blade have?
---
If you buy a blade from someone else, you might not know how many LEDs are in it, and unfortunately there is no way for ProffieOS to "just know" how many LEDs there are. Also, when you configure your blades, if you specify too few LEDs, the tip of the blade will not light up, and if you specify too may LEDs, effects which only light up the tip of the blade will not show, as they will light up LEDs that you do not have.

Fortunately, there is an easy way to find out how many LEDs your blade has. Add a new preset to your config file, and make the style for that blade this:

```cpp
StylePtr<LengthFinder<>>(),
```

Change the blade config to 144 LEDs, something like this:  

```cpp
WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
```

If you have COLOR_CHANGE_DIRECT in your config file, I recommend removing that temporarily while determining the blade length.
Now compile and upload.

Now, the LengthFinder<> style will light up a single LED, and speak the number of which one it is lighting up. So to start with it will say "one" and light up the first LED. Now, activate the color change mode. (Normally done with AUX+POWER, but may be different depending on your prop file). Now rotate the hilt, the LED will move, and the saber will speak the LED number every 3 seconds. All you need to do is to keep rotating until you find the point where the light reaches the tip and disappears, then rotate it back one step, so that the last LED of your blade is lit. At that point it will tell you how exactly how many LEDs are in your blade.

Now, go back to your config file, remove the LengthFinder<> preset, update your blade configuration with the length of your blade, compile, upload, and you're done.
