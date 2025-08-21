---
title: Sabersense Blade ID On Demand
---

Regular Blade ID works by performing an ID scan on bootup or font selection or other specific event, or by continuous ID scanning. The latter can sometimes result in momentary pixel flashes on the blade or neopixel connector, or false readings occasionally being returned which performs ID switches when you don't want them.
The Sabersense Blade ID system simplifies this by only performing blade ID scans on demand - simply triple-click the Power button and the saber will perform the scan and switch to the correct array for the blade. Note that you still need to set up the ID values in the same way you would with normal Blade ID. Details of how to do this can be found here: https://pod.hubbe.net/howto/blade-id.html

To use Sabersense Blade ID, add the following define to the CONFIG_TOP section of your config:

`#define SABERSENSE_BLADE_ID`

You will also need to add the following, with the LED power pins for your main blade specified:

`#ifndef ENABLE_POWER_FOR_ID PowerPINS<bladePowerPin2, bladePowerPin3>`
