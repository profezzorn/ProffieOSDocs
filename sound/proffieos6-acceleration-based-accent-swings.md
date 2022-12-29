---
title: ProffieOS v6.x acceleration-based accent swings
redirect_from:
  - /proffieos6-acceleration-based-accent-swings.html
---
In ProffieOS6 you can set your font up to use Accent Swings (swng.wav or swing.wav) based on swing acceleration.

Accent swings are played to give more life to faster swings on top of the normal swing pairs. Your font must include swng.wav or swing.wav files.

To do so your swng.wav sound files should be ordered sequentially with lowest file numbers for slower acceleration swings and highest numbers for fastest acceleration.

Acceleration Based Accent Swings will replace the need for Slashes, remove slsh.wav sounds from font or rename the slsh.wav files to swng.wav (or swing.wav) and use as the higher file numbers and combine with your Accent Swings to use this set up.

Example (files must be numbered sequentially you cannot skip a number or you will get "error in font directory"):
* swng01.wav - slowest Accent swing sound
* swng02.wav
* swng03.wav
* ...
* swng16.wav - fastest Accent swing sound


Then in the font config.ini you will add these variables:

> `#Minimum acceleration for Accent Swing file Selection`

> `#recommended value is 20.0 ~ 30.0`

> `ProffieOSMinSwingAcceleration=20.0`



> `#Maximum acceleration for Accent Swing file Selection`

> `#must be higher than Min value to enable selection`

> `#recommended value is 100.0 ~ 150.0`

> `ProffieOSMaxSwingAcceleration=100.0`

When these variables are present in the font config.ini -and- the MaxSwingAcceleration is greater than the MinSwingAcceleration the swng.wav files will be selected based on the actual acceleration of the swing event.
