SpiBladePtr can have up to 10 arguments, but only the first three are required.

    SpiBladePtr<leds, data_pin, clock_pin, byte_order, power_pins, max_frequency, pin_class, power_off_delay>

* leds - number of leds in this pixel string, must be less or equal to maxLedsPerSrtring
* data_pin - pin to output SPI data
* clock_pin - pin to output SPI clock
* byte_order - specifies in which orders the colors are sent to the pixels
* power_pins - which pads powers the string, defaults to PowerPINS<bladePowerPin1, bladePowerPin2, bladePowerPin3>
* max_frequency - maximum data rate, defaults to 800000
* pin_class - This is the driver class, defaults to SpiLedPin
* power_off_delay - milliseconds before turning off the power

data_pin and clock_pin is normally one of:

    bladePin
    blade2Pin
    blade3Pin
    blade4Pin
    blade5Pin
    blade6Pin
    blade7Pin

Other pins may or may not work depending on what board and driver is being used.

byte_order depends on what kind of pixel strip is used, these values are possible:
    
    Color8::BGR
    Color8::BRG
    Color8::GBR
    Color8::GRB
    Color8::RBG
    Color8::RGB
    Color8::BGRW
    Color8::BRGW
    Color8::GBRW
    Color8::GRBW
    Color8::RBGW
    Color8::RGBW
    Color8::WBGR
    Color8::WBRG
    Color8::WGBR
    Color8::WGRB
    Color8::WRBG
    Color8::WRGB
    Color8::BGRw
    Color8::BRGw
    Color8::GBRw
    Color8::GRBw
    Color8::RBGw
    Color8::RGBw
    Color8::wBGR
    Color8::wBRG
    Color8::wGBR
    Color8::wGRB
    Color8::wRBG
    Color8::wRGB

By far the most common byte order is GRB, but some pixel strips use RGB byte order. The four-letter byte orders are used for RGBW strips, the most common of those are GRBW and RGBW. The byte orders will capitol W will use both RGB AND W for white colors, while byte orders will lower-case w will only turn on the white LED for white colors. Thus RGBw is more power efficient than RGBW, but not as bright.
