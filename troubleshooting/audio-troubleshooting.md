---
title: Audio Troubleshooting
---
1. charge the battery and see if that helps
2. try "get_volume" in the serial monitor and make sure it's at least 1000, you can also try the "beep" command
3. With the board off, measure resistance across the speaker pads if you see....

     ... less than 1 ohm, you may have a short somewhere, or a broken speaker

     ... more than 10 ohm, you have a broken speaker

     ... 3-9 ohms, should be ok
4. With the board on, and while it's ignited, check the voltage between GND and the 5v pad, is it about 5 volts?  (If not, there is something wrong with the voltage booster.)
5. Switch your multimeter to AC measurements and measure between the speaker pads, do you see voltage when it's supposed to be playing? (And no voltage when it's not.) (If not, you may have a broken amplifier.)
