---
title: SD Cards
---
Most SD cards will work fine with ProffieBoards / TeensySaber.
Some very cheap cards, or cards below class 4 may cause issues with read speed.
Unfortunately, the problem usually doesn't show up in regular benchmarks since the Proffieboard and TeensySaber uses SPI mode instead of sdio to access the cards. This limits the speed, and some cards have a problem with it.

If you suspect that your SD card is causing problems, try the "sdtest" command.
This will read the hum file from your current font over and over again and see how long it takes.
Normal SD cards should give you 10-11 parallel streams. If you see less than 9, get a new SD card.

Please note that the "sdtest" command will not be available in the [Serial Monitor](../serial-monitor.html) if you have
DISABLE_DIAGNOSTIC_COMMANDS in your config file.
