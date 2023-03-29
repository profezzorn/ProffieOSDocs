---
title: How to set up a blaster
---

If you want to setup a blaster, first you have to understand the general mechanics.

A blaster is always on (unless a dedicated Power button is added).
The blaster.h prop offers three "modes": Stunt, Kill and Auto.
You have a certain number of shots until you need to reload.

First you need at least one blaster soundfont. There are some free soundfonts only a search away.
## List of Names and Effects
| Filename | Effect |
|---|---|
| `boot`               | `boot`    | Played when ProffieOS boots up. |
| `swing`              | `swng`    | Accent swing sounds that play near the peak of a swing motion.|


| `bgnauto` | Played when auto fire starts |
| `auto` | Played while auto fire is
| `endauto` | Played when auto fire ends |
| `blast` | 
| `clipin` | Sound made when inserting a clip |
| `clipout` | Sound made when dropping a clip |
| `empty` | Sound when the weapon is out of rounds |
| `fire` | Firing sound |
| `full` | Sound made when the weapon is full of ammo |
| `jam` | Sound made when the weapon jams |
| `unjam` | Sound made when unjamming the blaster |
| `mode` | Sound made when switching mode (OS 6+: when `mdkill`, `mdstun` and/or `mdauto` not present |
| `plioff` |
| `plion` |
| `range` | 
| `stun` | Firing sound for stun mode |
| `reload` | Reloading sound |
| `mdkill` | (OS 6+) Sound made when switching to KILL mode |
| `mdstun` | (OS 6+) Sound made when switching to STUN mode |
| `mdauto` | (OS 6+) Sound made when switching to AUTO mode |

Then comes the time to configure the board's `config.h`.
So, you will start by setting the `CONFIG_PROP` to use the `blaster.h` prop.
