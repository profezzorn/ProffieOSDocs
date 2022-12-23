SimpleBladePtr takes 8 arguments, 4 of which are required:

    SimpleBladePtr<LED1, LED2, LED3, LED4, pin1, pin2, pin3, pin4>

The first four are class names which specifies how to drive the LEDs, the last four are the pins for those leds.
The pins defaults to bladePowerPin1, bladePowerPin2, bladePowerPin3 and bladePin, respectively.

You can read more about how to configure the led classes on the [Led Configuration](led-configuration.md) page.
