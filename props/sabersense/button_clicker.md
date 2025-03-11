# The Button Clicker

## Overview
Some hilts, like KR's Scavenger hilt for instance, have complex switch systems that make it difficult to feel when the saber's switch is actually being pressed or released. This can make accessing certain features difficult.

For this reason, the Sabersense system offers a 'button clicker' feature.

Simply add this define to the CONFIG_TOP section of your config:

#define SABERSENSE_BUTTON_CLICKER

Then add two audio files to your font folder (or common/shared folder). These are available for download from the Sabersense website - www.sabersense.co.uk:
> press.wav

> release.wav

The system will now play those files to accompany each press and release of the button. This makes system navigation much easier.
