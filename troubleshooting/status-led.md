---
title: Desciphering the status LED
---

The V3 Proffieboard has a status led. That LED can provide a fair amount of information about what the board is doing. Let this page be your decoder wheel for understanding what it's doing.

## Blinks

If the LED is blinking (not pulsing) then it's trying to show you an error code. The number of blinks tells you what the error is, according to the following table:

1. Low Battery
2. SD Card Not Found
3. Error in Blade Array

## OFF

The LED will be off if the saber is completely idle in order to save power.

## Pulsing

When the saber is doing something, the saber will be pulsing. The speed of the pulse will tell you how busy the saber is. If it's pulsing fast, then the saber is working hard, if it's pulsing slowly, it is not. WHen USB is connected, the shape of the pulse will change from a triangle wave (/\/\/\/\) to a sawtooth wave (/|/|/|/|/|). When ignited, the brightness of the LED will increase.  When charging, there will be an extra "blip" every 2 seconds on the status LED.

## Controlling the LED yourself

If you don't like how the status LED behaves by default, you can add #define NO_STATUS_LED to your config file. Then you can add a blade to control the status LED like this:

```cpp
  SimpleBlade<CH1LED, NoLED, NoLED, NoLED, statusLEDPin, -1, -1, -1>()
```
