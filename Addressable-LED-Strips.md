
` WS2811BladePtr<97, WS2811_800kHz | WS2811_RGB, blade2Pin, PowerPINS<bladePowerPin1>>()`

1. First argument specifies the number of LEDs in the strip
2. Second argument specifies configuration options that are specific to the LED strip

Color order onfiguration options:
* WS2811_RGB
* WS2811_RBG 
* WS2811_GRB 
* WS2811_GBR  

Data clock rate configuration options:
* WS2811_800kHz
* WS2811_400kHz
* WS2813_800kHz
* WS2811_580kHz
* WS2811_ACTUALLY_800kHz

3. Data pin that is used to drive the specific LED strip:
* bladePin 
* blade1Pin (ProffieBoard)
* blade2Pin (ProffieBoard)
* blade3Pin (ProffieBoard)
* blade4Pin (ProffieBoard)
* blade5Pin (ProffieBoard)

On a teensysaber, pin 8 and 9 can be used if not used as a serial port.

4. FET transistor output that enables power to the LED strip:
* bladePowerPin1
* bladePowerPin2
* bladePowerPin3 
* bladePowerPin4 
* bladePowerPin5
* bladePowerPin6 

__If no option is set Pin Array object is created for bladePowerPin1, bladePowerPin2 and bladePowerPin3__

Addresable LEDs have 4 signals (WS2813 have additional bypass line)
* VCC
* GND
* DATA IN
* DATA OUT

The ProffieOS supports the following types:
* WS2812
* WS2812B
* WS2813
* PL9823 
* SK6812

***

## Protection

1. As the led strips get immense amount of current, it is good suggestion to use thick wires for VCC and GND to avoid heat/power loss. 
1. It is good practice to put large electrolytic capacitor  ( 470uF to 2200uF) as close as possible to the strip to avoid spontaneous current draws, that might occur. 
1. In order to protect the first addressable led in the chain from voltage spikes and additionally to make sure those spikes don't disrupt the integrity of the communication signal, a series resistor must be put as close as possible to the LED strip (100ohm to 470ohm)

***
## Neopixel
NeoPixel is Adafruit's brand of individually-addressable red-green-blue (RGB) LED. They are based on the WS2812 LED and WS2811 driver, where the WS2811 is integrated into the LED, for reduced footprint. The control protocol for NeoPixels is based on only one communication wire. 