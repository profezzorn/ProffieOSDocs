---
title: How to switch LED pads
---

Sometimes, a [FET](/glossary.html#fet) goes gets damaged. Or, maybe a solder pad gets ripped out, or something else happens that means that one of the LED1-6 pads can't be used anymore. In most cases, there is an unused LED pad or two that can be used instead. For now, let's assume that something bad happend to LED2 and LED3, and that we need to move the main blade over to use LED4 and LED5 instead.

The soldering part is fairly obvious, just cut or de-solder the wire from LED2/LED3 and solder it to LED4 and LED5 instead.

Now, we just need to update the blades array so that the Proffieboard knows to use the new pads. The blades array in the config file might look like this:

```
BladeConfig blades[] = {
 { 0, WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(presets) },
};
```

We just need to search & replace bladePowerPin2 with bladePowerPin4 and bladePoerPin3 with bladePowerPin5, so the results looks like this:

```
BladeConfig blades[] = {
 { 0, WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin4, bladePowerPin5> >(), CONFIGARRAY(presets) },
};
```

Upload ProffieOS to your saber using the updated config file, and everything should work just fine.

See also [how to test a FET](/troubleshooting/fet-testing.html) to find out how to check if a FET is not working.
