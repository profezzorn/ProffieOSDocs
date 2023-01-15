---
title: LED Channel Selection
---
If you have read the [LED Configuration](/config/blades/led-configuration.html) page, you know how ProffieOS activates channels based on colors. However, what is perhaps less obvious is how to use that in practice.

Let's start with the obvious case, an RGB three-cree star, using the recommended resistors:

`SimpleBladePtr<CreeXPE2RedTemplate<550>, CreeXPE2GreenTemplate<0>, CreeXPE2BlueTemplate<240>, NoLED>()`

In this case, the mapping between color and what channels are turned on is pretty obvious:
Red colors turns on the red LED, green colors turn on the green LED and blue colors turn on the blue LED.
But what if we replace the red led with an amber one?

Now, we have two choices, the first one is fairly obvious:
`SimpleBladePtr<CreeXPE2AmberTemplate<420>, CreeXPE2GreenTemplate<0>, CreeXPE2BlueTemplate<240>, NoLED>()`

However, the mapping between colors and channels now get more complicated. Green and blue works the way you
would expect, but red won't turn on anything.  The amber LED struct defines it's color as:

` static const int Red = 255;
  static const int Green = 128;
  static const int Blue = 0;
`
Going back to the [LED configuration](/config/blades/led-configuration.html) page, we can figure out that we would need to use a color like Rgb<255,128,0> to activate the amber LED. However, that color will also activate the green LED with 50% power, which might not be what we want.

However, there is another option: We can redefine what RGB means.
To do that, we'll need to copy the amber LED struct into our config file and change it to:

```cpp
template<int milliohms = 420>
struct MyCreeXPE2PCAmberTemplate {
  static constexpr float MaxAmps = 1.0;
  static constexpr float MaxVolts = 3.28;
  static constexpr float P2Amps = 0.35;
  static constexpr float P2Volts = 3.05;
  static constexpr float R = milliohms / 1000.0;
  static const int Red = 255;
  static const int Green = 0;  // This is the only thing that was changed
  static const int Blue = 0;
};
```

The we can use it:
`SimpleBladePtr<MyCreeXPE2AmberTemplate<420>, CreeXPE2GreenTemplate<0>, CreeXPE2BlueTemplate<240>, NoLED>()`

Now we're back at a state where the red activates the first channel, even though it's not really red.
So Rgb<255,0,0> now means amber, not red. Green and Blue still work as normal. Other colors will also become funky, because Purple will now activate amber and blue, and yellow will activate amber and green. Not sure exactly what these colors will look like, but they won't be purple and yellow.

This trick can be applied to any of the channels. Note that this trick will not really work properly if you have four different LEDs on your star, and you want to control all of them. RGB only has three values in it after all.
