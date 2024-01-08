---
title: The history of clash detection in ProffieOS
---

In the beginning, there was `CLASH_THRESHOLD_G`.

Originally, the clash algorithm would simply compare the new accelerometer value with the last accelerometer value, and if it was greater than `CLASH_THRESHOLD_G`, it would trigger a clash, like:

$|Acceleration_{now} - Acceleration_{last} | > CLASH\textunderscore THRESHOLD\textunderscore G $

Note that the acceleration values are vectors with X, Y and Z components, and the || takes the length of the vector. In other words, this is the same as doing:

$X = XAcceleration_{now} - XAcceleration_{last}$

$Y = YAcceleration_{now} - ZAcceleration_{last}$

$Y = YAcceleration_{now} - ZAcceleration_{last}$

$\sqrt{X^2 + Y^2 + Z^2} > CLASH\textunderscore THRESHOLD\textunderscore G$

The problem with this algorithm is that the frequency of readings changes what it does. If you get more readings per second, then the difference between each one will be smaller, so the same CLASH_THRESHOLD_G wouldn't work. Back then, Proffieboards were new, and there were lots of Teensysabers still around, and because of differences in how they worked, they would often get different number of readings per second.

So a long long time ago, I changed this algorithm, instead of using the "last" value, I used a slow average of values instead, so the algorithm became:

$| Acceleration_{now} - Acceleration_{average} | > CLASH\textunderscore THRESHOLD\textunderscore G $

In ProffieOS 3, this algorithm was improved by adding the Fusor class. The Fusor uses the accelerometer and the gyro to calculate a down vector. When nothing is happening, the down vector and the accelerometer should be the same thing.  But this allowed me to change the algorithm to:

$| Acceleration_{now} - Down | > CLASH\textunderscore THRESHOLD\textunderscore G $

So far, the improvements have been just that: improvements, however, at this point the story takes a bit of a turn... I discovered two potentially problematic things.

1. The range for acceleration values was set to -4 to 4. Values higher than this would be truncated by the motion chip. For some reason though, many people seemed to find that they needed values around four for clash detection to work well for them. Values around 3.9 were quite common for some reason. To me, that meant that the algorithm wasn't really working as designed. Also, it gets a little wonky, because the truncation is cube-shaped, so if you hold your saber at a 45 degree angle, then the maximum value would be $ \sqrt{3 * 4^2} = 6.9 $ and having an algorithm that works differently depending on the angle didn't seem like a good idea.
2. The accelerometer was set to 1600 readings per second. However, because of implementation details, we were usually only getting 800 readings per second, but sometimes it was much less, if your saber had lots of blades, OLED displays and stuff.  A related problem was that OLED displays were updating slowly when the saber was on.

So I implemented an interrupt-driven i2c handler, which lets us reliably read 1600 accelerometer reading per second, and I also changed the range of values returned by the accelerometer from 4 to 16. Both of these seemed like a good idea, more and better data, right?

This turns out to not always be the case.

It turns out that when you sample the accelerometer very quickly, sound has a bigger impact on the readings. In the past, readings got *smaller* when I read the accelerometer more often, but this time, they got *bigger*, which causes more false clashes. Also, whatever fluke made the 3.9 values work well disappeared because I changed the range to 16.

In order to figure out what was going on, I added some defines to control the speed and range of accelerometer readouts:

```
#define PROFFIEOS_ACCELEROMETER_RANGE 16
```
This one can be set to 2, 4, 8 or 16, and specifies the range of values measured by the accelerometer. Higher values means less precision, but we don't really need high precision, so it doesn't really matter. However, if you want the 3.9-value-fluke, you should set this to 4.

```
#define PROFFIEOS_MOTION_FREQUENCY 1600
```
This define controls how often we read the accelerometer. I don't remember exactly what all the valid values are, but the interesting ones are basically 800 and 1600. The default is 1600, 800 is basically what ProffieOS 5 and below would get.

Once we started figuring out what was going on. We also added some potential solutions to the problem. In ProffieOS 6 there were two changes meant to solve this problem. The first one is a filter that averages the clash values over a short period of time to try to get rid of the high values that sometimes comes from sound. This filter is controlled by this define:

```
#define ACCEL_MEASUREMENTS_PER_SECOND 800
```

The default is 800, and the code just creates a box filter of size (PROFFIEOS_MOTION_FREQUENCY / ACCCEL_MEASUREMENTS_PER_SECOND = 2) to do the averaging. Setting this define to the same value as PROFFIEOS_MOTION_FREQUENCY (1600) means that no filtering will occur. Setting it to a lower value is also valid, but will cause some (very minor) latency in clash detection.

The other solution is:
```
#define AUDIO_CLASH_SUPPRESSION_LEVEL 10
```
This define checks the volume of sound currently being emitted and increases the CLASH_THRESHOLD_G accordingly. Higher values means more suppression when the volumes goes up, but that also means it's more difficult to actually make a clash happen.

Together these two things worked fairly well, but some people still had problems, and lots of people found that their old CLASH_THRESHOLD_G values were too low, and had to increase them to 5-7 for things to actually work. This wasn't really my intention, but that's what happened.

At some point after releasing ProffieOS 6, Fett263 told me that he used the *gyro* to detect clashes in his blade code.  I'm like you do *what*? Here I had been using the accelerometer for years, and it turns out there is different way...

So I did a bunch of experimentation, and I found that the gyro values tends to spike when a clash occurs. This makes sense, because there is a change in rotation when the blade hits something. However, I found that the type of clash would affect the size of  the gyro spike quite a bit, making it not always reliable. However, if I used *both* the gyro and the accelerometer, I got a clash detector that seemed to work much better than either one individually.

The formula is basically:

$| accel - down |/2+ | \Delta gyro|/2 > CLASH\textunderscore THRESHOLD\textunderscore G $

For many people, this formula works really well, and it helps filter out most of the false clashes. However, for some people, this formula seems to be the opposite of helpful, forcing them to increase their clash threshold and make clashes harder to trigger. I'm not sure why that is though, but somehow the clash spike and the acceleration spike must not arrive at the same time.

Anyways, I made a define for disabling this new formula and use the previous one:

```
#define PROFFIEOS_DONT_USE_GYRO_FOR_CLASH
```

For some people the old formula works better, and they need this define.

That's it.
Almost.

There is one detail I left out, because I don't remember when I added it, and there is no define to control it. (It was a long time ago though.)

There is a piece of code in there that checks the swing speed, and increases the clash threshold accordingly. Before I added this, false clashes during swings were very very common. That code lives here:

https://github.com/profezzorn/ProffieOS/blob/3bfcc59d7a831bc4fcc7ed1e1b5bbd70ec73ee34/props/prop_base.h#L823C34-L823C60

