---
title: How to test if data pins are working.
---

If your WS281X pixels don't light up, it's often hard to know why. It could be the data, it could be the power, or a burnt out pixel. To test the power, see [the FET testing](/troubleshooting/fet-testing.html) page. To check if the data is working, keep reading.

1. get a multimeter
2. set it to measure AC voltage
3. Put one probe on the GND pad on the board
4. Put the other one on the data pad you want to test.
5. Check the measurement.

If data is flowing, you should see a fluctuating value somewhere around one volt. The actual value will depend on the color, and also on the meter. It's not very important what the value is, as long as you see a distinct difference when data is flowing and data is not flowing.

Data should be flowing when the board is on and ignited unless you use styles which allows the blade to turn off, like `StylePtr<Black>()` in your config file. If data is not flowing there are a couple of things to check:

* the config file might have an error in it causing the blade to not work. To rule this out, replace your config file with a super-simple one, like the default_proffieboard_config.h, or one that comes from the proffieboard configurator.
* There may be a short somewhere permanently making that particular pin fixed at a particular voltage. Try checking for continuity between the data pin and GND, 3.3v or BATT+.
* The pin is burnt out and you should try a different one.

To try a different one, you will need to update your config file to use the new pin. Let's say your blades[] array looks like this:

```
BladeConfig blades[] = {
 { 0, WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(presets) },
};
```

To change it to use the Data2 pin instead of Data1, you should change the blades array to:
```
BladeConfig blades[] = {
 { 0, WS281XBladePtr<144, blade2Pin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(presets) },
};
```
Note that Data2 does not have a built-in resistor like Data1 does, so you will need to add a resistor when switing from Data1 to Data2.
