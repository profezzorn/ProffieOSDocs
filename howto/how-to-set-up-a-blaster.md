---
title: How to set up a blaster
---

#Blaster Setup HOW-TO

## Introduction
If you want to setup a blaster, first you have to understand the general mechanics.

A blaster is always on (unless a dedicated Power button is added).
The blaster.h prop offers three "modes": Stunt, Kill and Auto.
You have a certain number of shots until you need to reload.

First you need at least one blaster soundfont. There are some free soundfonts only a search away.

## List of Names and Effects
| Filename | Effect |
|---|---|
| `bgnauto` | Played when auto fire starts |
| `auto` | Played while auto fire is
| `endauto` | Played when auto fire ends |
| `blast` |
| `boot` | Played when ProffieOS boots up. |
| `clipin` | Sound made when inserting a clip |
| `clipout` | Sound made when dropping a clip |
| `empty` | Sound when the weapon is out of rounds |
| `fire` | Firing sound |
| `font` | Name of the preset |
| `full` | Sound made when the weapon is full of ammo |
| `hum` | Constant sound looping while not firing |
| `jam` | Sound made when the weapon jams |
| `unjam` | Sound made when unjamming the blaster |
| `mode` | Sound made when switching mode (OS 6+: when `mdkill`, `mdstun` and/or `mdauto` not present) |
| `plioff` | Played while retracting the PLI bargraph. | 
| `plion` | Played while extending the PLI bargraph. |
| `range` |  Up to 16 sounds of increasing weapon range/power |
| `stun` | Firing sound for stun mode |
| `reload` | Reloading sound |
| `mdkill` | (OS 6+) Sound made when switching to KILL mode |
| `mdstun` | (OS 6+) Sound made when switching to STUN mode |
| `mdauto` | (OS 6+) Sound made when switching to AUTO mode |

*If `mdkill`, `mdstun`, `mdauto` nor `mode` are present Talkie voice speaks selected mode.*

## Configuration

Then comes the time to configure the board's `config.h`. You should start by adding to your `CONFIG_TOP` section the following defines

```
/****** CONFIG_TOP blaster defines  ****/
#define ENABLE_BLASTER_AUTO           // If you desire to enable AUTO mode.
#define BLASTER_SHOTS_UNTIL_EMPTY 15  // The capacity of your weapons rounds.
#define BLASTER_JAM_PERCENTAGE 1     //  0-100. If not defined, random.
```

So, you will start by setting the `CONFIG_PROP` to use the `blaster.h` prop.

```
/****** CONFIG_PROP blaster defines  ****/
#include "../props/blaster.h"
```
