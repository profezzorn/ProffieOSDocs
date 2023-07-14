---
title: Blade ID
redirect_from:
  - /blade-id.html
---
So you know that first number in the blade configuration?  
Do you know what it's for?  
It's the Blade ID.

When ProffieOS starts, it measures the resistance between the Blade ID pin (which is usually the same as the neopixel data pin for the first blade) and GND. It then finds the entry in the blades table with the closest first number, and then it uses that entry until the next time it scans for a blade. This may be at power on, or triggered by [Blade Detect](blade-detect.html).
An example of a BladeConfig with multiple, different resistor value blades is shown here:
```cpp
 BladeConfig blades[] = {
      { 5000,
        WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
        CONFIGARRAY(blade1_in) },
      { 10000,
        WS281XBladePtr<128, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
        CONFIGARRAY(blade2_in) },
      { NO_BLADE,
        WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
        CONFIGARRAY(no_blade) },
    };
```
 
So how do you use this?  
Well, the idea is that if you have multiple blades, you can place a resistor between the data pin and GND, and ProffieOS can use that resistor to identify which blade is connected. In the simplest possible case, this could be used to support WS281X blades of different lengths, but it's also possible to support entirely different types of blades, assuming your blade connector has enough pins.

Note that the Blade ID resistor is different from the in-line resistor normally used for WS281X blades. The resistors are also different sizes. The in-line resistor should be 150-470 ohms, but the Blade ID resistor should be somewhere in the 2k to 100k range. Any lower may interfere with the blade data.

The V1 electronics is still one of the best pictures for showing how this can work: [https://fredrik.hubbe.net/lightsaber/electronics.html](https://fredrik.hubbe.net/lightsaber/electronics.html)

Unfortunately, it turns out that Proffieboard V1.5 and V2.2s are unable to do Blade ID in the same way as TeensySabers do, because there is no way to enable a pullup/pulldown resistor while doing an analog read from the pin. Several workarounds exist for this in ProffieOS 3.x.  
*NOTE* - These are not needed for a Proffieboard V3.
V3 already has what it needs internally.  

The first option would be adding this to the config file:

```cpp
#define BLADE_ID_CLASS SnapshotBladeID<bladeIdentifyPin> 
```

The default blade ID class (SnapshotBladeID) charges up the internal sampling capacitor, then connects the sampling capacitor to the Blade ID pin for a *very* short time, and then does the analog-to-digital conversion. This should give consistent values for the same blade, but unfortunately, the values will not reflect the value of the Blade ID resistor, so the blades array has to be configured with measured values, not with values based on the resistor in the blade. Measured values can be found by using Serial Monitor in Arduino, and entering `scanid` while the blade is off.

Alternatively, an external pull-up resistor can be used. This resistor should be in the 20k to 50k range and placed between the blade pin and 3.3v. Then you add this to the config file:

```cpp
#define BLADE_ID_CLASS ExternalPullupBladeID<bladeIdentifyPin, 22000>
```

(Replace 22000 with the value of your pullup resistor.) With this workaround, Blade ID should return values that are close to the Blade ID resistor values, which will make configuration easier.

Another option is to bridge the blade pin with another pin and use that pull-up resistor. On a Proffieboard V2.2, the ID pin is right next to the TX pin. If you bridge those two together, and put this is your config file:

```cpp
#define BLADE_ID_CLASS BridgedPullupBladeID<bladeIdentifyPin, 9>
```

(9 is the pin number for the TX pin) Then Blade ID should also return the values of the resistors. However, this means that you can't use the TX pin for anything else of course, such as a Bluetooth radio.

Another quirk of Blade ID is that unpowered neopixels throws it off. When the neopixels are powered, the inputs are high impedance, which doesn't affect the Blade ID, but when unpowered, they leech power from the data line, which throws off the Blade ID value. The solution is to turn the power on while we're doing Blade ID by using the ENABLE_POWER_FOR_ID define. If your blade is hooked up to the LED2 and LED3 pads, it would look like this:

```cpp
#define ENABLE_POWER_FOR_ID PowerPINS<bladePowerPin2,bladePowerPin3>
```

*IMPORTANT NOTE* - BladeID requires a direct, uninterrupted connection from the board's data pin to the main blade (usually the center pin on the hilt-side of the main blade PCB). Therefore using SubBlades with neopixel accents, crystal chamber, or NPXL LED PCBs in series with the main blade won't work. They can be their own SubBlade chain on a data pin other than data1, but only data1 can use BladeID.  

As of ProffieOS7, a new method of detecting different "blades" by using Blade ID is available.  
See [Blade ID constant monitoring](blade-id-constant-monitoring.html).
