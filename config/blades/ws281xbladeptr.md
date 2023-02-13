---
title: WS281XBladePtr
---
WS281XBladePtr can have up to 10 arguments, but only the first three are required.

    WS281XBladePtr<leds, data_pin, byteorder, power_pins, pin_class, frequency, reset_us, t1h, t0h>

* leds - number of leds in this pixel string, must be less or equal to maxLedsPerSrtring
* data_pin - pin to output ws281x data
* byte_order - specifies in which orders the colors are sent to the pixels
* power_pins - which pads powers the string, defaults to PowerPINS<bladePowerPin1, bladePowerPin2, bladePowerPin3>
* pin_class - This is the driver class, defaults to DefaultPinClass
* frequency - data rate, defaults to 800000
* reset_us - how many us is needed to reset the pixels, defaults to 300
* t1h - how long to keep the signal high for a 1, note that this is is always out of 1200, even if the frequency changes, defaults to 394
* t0h - how long to keep the signal high for a 0, defaults to 894

data_pin is normally one of:

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

By far the most common byte order is GRB, but some pixel strips use RGB byte order. The four-letter byte orders are used for RGBW strips, the most common of those are GRBW and RGBW. The byte orders with a capital W will use both RGB AND W LEDs for white colors, while byte orders with lower-case w will turn on only the white LEDs for white colors. Thus RGBw is more power efficient than RGBW, but not as bright.

Most of the time it does not make sense to change the pin_class, but if you have a Teensy, and you have problems with glitches, you might want to try the serial pixel driver by setting pin_class to WS2811SerialPin. You'll also need to use a data pin that is serial-capable, which may mean that you can't use the serial port for something else. Note that WS2811SerialPin ignores t0h and t1h.

It's unlikely that you will need to change any of the last four parameters, the timing is suitable for almost all types of WS2811-compatible pixels.

