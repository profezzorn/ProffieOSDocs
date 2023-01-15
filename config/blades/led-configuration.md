---
title: LED Configuration
---
When using SimpleBladePtr<> or StringBladePtr<> in your blade array, you have to provide a led configuration class. That class specifies the color and electrical properties of the LED.  If the color returned by the style matches the color specified in the led configuration, the LED will be activated.  If the current battery voltage is higher than what is specified in the electrical properties, the LED brightness will be reduced to avoid overheating the LED.

## Example LED configuration class

```cpp
struct MyBlueLED {
  static constexpr float MaxAmps = 1.0;
  static constexpr float MaxVolts = 3.15;
  static constexpr float P2Amps = 0.7;
  static constexpr float P2Volts = 3.05;
  static constexpr float R = 0.55;
  // LED color
  static const int Red = 0;
  static const int Green = 0;
  static const int Blue = 255;
};

MaxAmps should be the maximum current that the LED allows. In this case, 1.0A.
MaxVolts is the forward voltage at which you get the maximum number of amps. In this case 3.15 volts.
"P2" stands for "second point", and P2Amps/P2Volts specifies another point on the amp/volt curve. In the case above, it says that at 3.05 volt, the LED will draw 0.7 Amps.

Generally, MaxAmps can be found in the data sheet for the LED. And while you can also get the other values from the data sheet, it is preferable to measure them, as the forward voltages can vary from led to led and a small amount of difference in voltage can mean a fairly large difference in current.

The "R" value, specifies what resistor is hooked up in series with the LED. In this case 0.55 ohms.

Finally, the Red, Green and Blue values specifies the color of the LED.

## Color Activation
ProffieOS uses a simple formula to determine how much a LED should be turned on given a particular color from style associated with that LED. The formula is:

```cpp
activation = 255;
if (LED.Red) activation = min(activation, color_from_style.red * 255 / LED.Red);
if (LED.Green) activation = min(activation, color_from_style.green * 255 / LED.Green);
if (LED.Blue) activation = min(activation, color_from_style.blue * 255 / LED.Blue);
```

This essentially means that for the blue led in our example, only the blue part of the RGB color is considered when deciding how much the LED should be activated. This also means that Cyan, Purple and White will also activate the Blue LED, which is usually what we want.  A LED specified as being White, will only be activated when for White colors. For a color like {10, 20, 30}, the min() means that a white LED will have it's activation set to 10 (out of 255).  For an RGB star, three LED definitions are used, and the activation for each channel is calculated separately according to the above formula.

This formula is not well suited for color accuracy. A matrix multiplication could be used instead to get proper color accuracy and account for the fact "blue" can mean different things for different LEDs. While this formula does not provide that type of color accuracy, it is much simpler and generally chooses the brightest possible value, which I think is more suitable for a lightsaber.

## Using SUBTRACT
One problem with the activation formula above is that if you have a Blue/Blue/White LED, there is no way to
get a pure white color, because the Blue LEDs will also be activated. To remedy this, we can introduce subtraction into the activation formula. To do that we place the following in the blue LED struct:

```cpp
typedef MyWhiteLED SUBTRACT;   // MyWhiteLED is the name of the led struct used for the white LED
```

When you do this, ProffieOS will calculate the activation as shown above, then calculate the activation based on the white color and subtract that, sort of like:

```cpp
activation = CalculateActivation(MyBlueLED) - CalculateActivation(MyWhiteLED)
```

With this setup, the blue led will turn on for blue colors, but turn off for white colors. This can also be used as a power-saving feature for RGBW stars to make it so that only the white die is used for white colors. Otherwise all of the dies will turn on for white colors. Here is how you would do that:

```cpp
struct MyWhiteLED : public CreeXPE2WhiteTemplate<550> {};
struct MyRedLED : public CreeXPE2RedTemplate<1000> { typedef MyWhiteLED SUBTRACT; };
struct MyGreenLED : public CreeXPE2GreenTemplate<0> { typedef MyWhiteLED SUBTRACT; };
struct MyBlueLED : public CreeXPE2BlueTemplate<240> { typedef MyWhiteLED SUBTRACT; };

BladeConfig blades[] = {
  { 0,  SimpleBladePtr<MyRedLED, MyBlueLED, MyGreenLED, MyWhiteLED,
                       bladePowerPin1, bladePowerPin2, bladePowerPin3, bladePowerPin4>(), 
    CONFIGARRAY(presets) }
};
```

Note the use of "struct SOMETHING : public SOMETHING_ELSE { .... }" this creates a new struct, but copies the content of SOMETHING_ELSE into it. If you decide to use the snipped above in your config file, please make sure to adjust the resistors to the values you are actually using.


## Overheat protection
ProffieOS will use MaxAmps, MaxVolts, P2Amps, P2Volts and R to estimate the current flowing through the LED, based on the current battery voltage. This is done using a fairly simplistic affine model of the LED. Basically, imagine that you draw a current/voltage graph for the LED, locate the MaxAmps/MaxVolts and P2Amps/P2Volts points and draw a straight line through them. Based on this line, and R, the current can be estimated. If the estimated current comes out to be 20% higher than what is recommended for the LED, the activation value calculated above will be reduced by 20% to compensate. This works well enough that resistors are not always required to drive LEDs using ProffieOS, however, it may reduce the life span of the LED.

Stated differently, if the above algorithm shows that the led would end up using more power than the LED struct specifies, the PWM ratio (the fraction of time that the FET is ON for each 800Hz cycle) is adjusted downwards to try to protect the LED.

Note that if any of the values are not specified correctly, the LED may dim because ProffieOS thinks the LED is going to overheat. Or, overheat-protection might not work. If you don't want the overheat protection, because it is too difficult to configure, just specify a very high R and MaxVolts values and ProffieOS will always assume the LED will be fine.

## Templated LED configuration
Many popular LEDs already have LED configuration structs in blades/leds.h. Since people have their own preferences for what resistors to use, they are generally specified as templates, which lets you specify what resistor you actually used as a parameter in milliohms. (Unfortunately, specifying it in Ohms was not an option as templates cannot handle floating-point values.)  For example, using `CreeXPE2PCAmberTemplate<240>` specifies that you have a CREE XP-E2 amber LED, and you have it hooked up in series with a 0.24 ohm resistor.

## Implications
* If you specify the wrong led struct, or the wrong resistor, the above doesn't work the way it should.
* If you tell ProffieOS that you have less resistance than you really have, ProffieOS will dim the LED when it shouldn't.
* If you don't need or want overheat-protection (perhaps because your resistors take care of that part) then you can disable it by putting in a large resistor value, like for instance 100000.

## Calculating resistor values
Calculating resistor values for LEDs is very simple.
I could give you the formula, but why bother when there are [simple calculators available online](https://ledcalculator.net/).

## Adding/Modifying LED structs
While you are welcome to add your own LED configuration structs to blades/leds.h, I recommend putting them in your config file instead, right before the blades[] array. That way, you won't have to remember to copy them over when you update to a new version of ProffieOS.

