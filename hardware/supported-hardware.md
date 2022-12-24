---
title: Supported Hardware
redirect_from:
  - /supported-hardware.html
---
While the Proffie OS was developed, a couple of hardware variants followed it. They are all PCB extensions of the Teensy 3.2 Development board. 
ProffieBoard is the latest variant using its own dedicated CPU and removing the need of "Sandwitch build" installs.

## Selecting hardware
To configure your program to run on specific hardware make sure to have its include header in your configuration file:
* `#include "v1_config.h"`
* `#include "v2_config.h"`
* `#include "v3_config.h"`
* `#include "proffieboard_v1_config.h"`
* `#include "proffieboard_v2_config.h"`
***
## Teensy Saber V1
![Teensy + Prop Shield (v1)](https://fredrik.hubbe.net/lightsaber/ratsnest.jpg)
## Teensy Saber V2
![TeensySaberV2](https://fredrik.hubbe.net/lightsaber/v2/TeensySaberV2.2.jpg)
## Teensy Saber V3
![TeensySaberV3](https://fredrik.hubbe.net/lightsaber/v3/TeensySaberV3Front.jpg)
## ProffieBoard V1.5
![ProffieBoard](https://fredrik.hubbe.net/lightsaber/v4/_DSC1630_CROPPED.JPG)
## ProffieBoard V2.2
![ProffieBoard](https://fredrik.hubbe.net/lightsaber/v5/pbv22.jpg)


