---
title: PQOIML
---

The PQOI markup language is very simple, here are all the possible commands:

### fps A:B

Specifies the frame rate as a fraction, here are some examples:

```
fps 25:1  # 25 fps
fps 24000:1001 # common movie frame rate (23.976 fps)
fps 30000:1001 # NTSC frame rate (29.97 fps)
```

### file FILENAME

Imports the image or movie into the PQF. Uses the scaling pipeline to scale each image.

### label LABEL

Generate a label. Labels don't actually exist in the output file, as GOTO and IF statements just use positions in the file instead.

### goto LABEL

Generates an unconditional jump to the label. Looped animations have goto to the beginning at the end.

### if COND goto LABEL

In pqoiml, if statements are very simple, they work just like a goto, but with a condition. The conditions are application defined, but are always exactly four characters long. The list of conditions supported by ProffieOS has not yet been finalized, but this is what is supported so far:

* ison - do the jump if the saber is ignited
* lock - if we're in normal lockup mode
* drag - drag lockup mode
* melt - melt lockup mode
* A<30 - if A is less than 30
* A>30 - if A is greather than 30
* A=30 - if A is equal to 30

Note that "A" is a generic variable, and the meaning of A can be assigned at runtime by using a .SCR file. There are 5 possible variables: A, B, C, D, E and their values can be battery percent, volume, and other things. There is also a special R variable which has a random value between 0 and 100.


### scaling SCALING PIPELINE

This sets the commands that scales the images. The scaling command is not saved in the output file, it's only used when a "file" statement is encountered. The scaling pipeline can also be specified on the command line, which makes it possible to use the same pqoiml file to generate multiple PQF files in different resolutions.

## An example pqoiml file:

This is a pqoiml file for a simple battery overlay:

```
scaling pamcut -pad 0 0 174 250 | pamflip -r180 | pamcut -pad 0 0 1280 640 | pamflip -r180 | pamscale -xysize 160 80

fps 1:2

label empty
file 0.png
label twenty
file 20.png
if A<10 goto blink
if A<40 goto twenty

label forty
file 40.png
if A<40 goto twenty
if A<60 goto forty

label sixty
file 60.png
if A<60 goto forty
if A<80 goto sixty

label eighty
file 80.png
if A<80 goto sixty

label full
if A<90 goto eighty
file 100.png
goto full
```
