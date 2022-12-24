A sound font is mostly made up of many sound files in a single directory. Let's take a look at the following example and break down the important aspects.

![font1/clash/001.wav](../images/font1_clash_001_wav.png)

This file name is made up of four main parts:

* The directory (Yellow) - This can be anything you want, and is typically the name of the font. All sound and config files must be in the same final directory, but fonts can be organized in to as many sub-directories as you want. The first entry in the [presets\[\] array](the-config_presets-section.md) specifies the full path to the font directory. For example, you can have your fonts sorted as `sith\1\sith1`, or `fonts\jedi\named\obiwan`, etc.
  * Note: While Proffie-based boards support long filenames, Teensy-based boards support a maximum of 8 characters for folder names. It is recommended to stick to this maximum to ensure full compatibility with any sound board. 

* The name (Magenta) - This is the name of the sound type, using the names specified below in the [Sound Effect Names](#sound-effect-names) section. In this example, it's a clash sound.

* The number (Cyan) - If you want to have multiple sound effects of the same type, add a number to the end of the filename before the extension. The numbers can be in the following format:
  * 1,2,3, etc.
  * 01, 02, 03, etc.
  * 001, 002, 003, etc.

  The number sequence must be consistent and without any gaps. It's also possible to omit the number completely if there is only a single sound. When playing a sound, ProffieOS will generally pick one of them randomly. For looping sounds, ProffieOS will randomly pick one of the numbered files each time it starts over. This means it's possible to create a more interesting hum by having `hum.wav`, `hum1.wav`, `hum2.wav`, etc.
  * Note: While Proffie-based boards support long filenames, Teensy-based boards support a maximum of 8 characters for file names. It is recommended to stick to this maximum to ensure full compatibility with any sound board.

* The extension (Pink) - The recommended format is .wav files that are 44khz, 16-bit mono PCM. ProffieOS also supports 11khz, 22khz, and 44khz .wav in both mono and stereo. You may also use .raw and .usl files, but they must be 44khz mono.

## Alternative font file naming
Instead of font1/NameNNN.wav, you can also use font1/Name/NNN.wav, which lets you have more files and better organization. font1/Name/NameNNN.wav is also supported for compatibility with Igniter boards.

## Font Search Paths.
You can have ProffieOS look in multiple directories for font and animation files, as well as config.ini and smoothsw.ini files.
Primarily, this is meant to make it easier to share files like "ccbegin" and "ccend" between fonts, but it can also be used for more advanced things, like adding different quotes to a font. 
So how do you use this? Basically, you just specify a list of directories with a semicolon in between.

So if your current preset says "font1", you could change it to "font1;common" to have it first search "font1", and any files found there will be used first. After that ProffieOS will search "common" and add any files not already found.
A prime example of how this can be used is the "hero" font pack. You could have one "hero/font;hero/obiwan;common" preset, and another "hero/font;hero/luke;common" preset, without having to duplicate the files in the "hero/font" directory.
<br/>Currently, the only limit on how many directories you can search is that the whole list of directories must be less than 127 characters.<br/>
One caveat, you can't mix files with the same base name.
Let's say hero/font contains preon01.wav. Even if hero/obiwan contains preon02.wav, it will not be used.
The decision of which directory to use is done _once_ for all files with the same "name", individually for each numbered file. 

**Note** This feature is only available in ProffieOS 4.x. and later.

## Sound Effect Names
The name part of the filename needs to be one that ProffieOS can recognize. Sounds can either be monophonic (Plecter) or polyphonic (Naigon Electronics) style. ProffieOS will automatically decide if a specific sound type is monophonic or polyphonic font based on the filename. Monophonic sounds will smoothly join with the hum when they are finished playing. Polyphonic sounds will automatically mix with the hum sound. Keep in mind that you cannot mix mono and polyphonic sounds for the same effect. For example, if you are using `clash`, you cannot use `clsh` as well. You can, however, mix for different effects. You could use `clash` alongside `blst` in the same font for example.

The following sounds are triggered along with blade animations. The buttons, gestures, or actions used to trigger them is specific to the prop file being used.  
See [The-CONFIG_PROP-section](The-CONFIG_PROP-section) for a list of prop files included with ProffieOS. Additional sounds are available when using some props, such as `quote`. Each prop will have instructions in the top comment section for how to use it.  If you are using the default saber.h prop, you can also read [How to use ProffieOS](How-to-use-it) for more details.

#### List of Names and Effects
| Monophonic Filename | Polyphonic Filename | Effect |
|---|---|---|
| `boot`               | `boot`    | Played when ProffieOS boots up. |
| `swing`              | `swng`    | Accent swing sounds that play near the peak of a swing motion.|
| N/A                  | `swingl`  | If present with `swingh`, the [SmoothSwing algorithm](#smoothswing-configuration) will be used to generate swing sounds from these files when the saber is moved around. |
| N/A                  | `swingh`  | If present with `swingl`, the [SmoothSwing algorithm](#smoothswing-configuration) will be used to generate swing sounds from these files when the saber is moved around. |
| `hum`                | `hum`     | Played when the saber is on and stationary (looped) |
| `poweron`            | `out`     | Extension sound when you ignite the blade. |
| `poweroff`, `pwroff` | `in`      | Retraction sound when the blade is shut off. |
| `clash`              | `clsh`    | Played when you hit something with the saber |
| `force`              | `force`   | Force use sound.|
| `slsh`               | `slsh`    | Played when you make a swing that is accelerating faster than the threshold set in either config.ini or smoothsw.ini (OS3.x and up) |
| `stab`               | `stab`    | Played when you make a stabbing motion (OS3.x and up) |
| `blaster`            | `blst`    | Blaster deflection sound. |
| `lockup`             | `lock`    | Sound when blades come together and struggle. |
| `bgnlock`            | `bgnlock` | Played when lockup starts |
| `endlock`            | `endlock` | Played when lockup ends (if not present, clash is used) |
| `drag`               | `drag`    | Sound for dragging the tip of the saber blade. |
| `bgndrag`            | `bgndrag` | Begin drag |
| `enddrag`            | `enddrag` | End drag |
|                      | `lb     ` | Force lightning block. |
|                      | `bgnlb`   | Begin lightning block. |
|                      | `endlb`   | End lightning block. |
|                      | `melt`    | Simulate stabbing and melting an object with blade tip.|
|                      | `bgnmelt` | Begin melt |
|                      | `endmelt` | End melt |
| `poweronf`           | N/A       | Force power on. (not yet implemented in ProffieOS) |
| `font`               | `font`    | Played when you switch to this preset. |
|  N/A                 | `ccbegin` | Played when entering color change mode. |
|  N/A                 | `ccend`   | Played when exiting color change mode |
|  N/A                 | `ccchange` | Played when changing color in "stepped" color change mode |
| `preon`              | `preon`    | Played before the blade turns on |
| `pstoff`             | `pstoff`   | Played after retraction when the blade turns off |

#### Thermal Detonator Props
* `bgnarm` - when the td is arming
* `armhum` - when the td is armed (looped)
* `endarm` - when the td is disarmed
* `boom` - when the td blows up

#### Blaster Props
* `bgnauto`
* `auto`
* `endauto`
* `blast`
* `clipin`
* `clipout`
* `empty`
* `fire`
* `full`
* `jam`
* `unjam`
* `mode`
* `plioff`
* `plion`
* `range`
* `stun`
* `reload`  
As of OS6:
* `mdkill`
* `mdstun`
* `mdauto`

## SmoothSwing Configuration
When one or more set of `swingl`/`swingh` files are present, ProffieOS will activate the SmoothSwing algorithms. To decide if it should use V1 or V2, it will read a file called "smoothsw.ini". More information on how to configure this file can be found on [the smoothswing page](smoothsw.ini).

#### SmoothSwing V1
[Demo Video](https://www.youtube.com/watch?v=4AAYGw09bu0) ([Thexter's description](https://www.fx-sabers.com/forum/index.php?topic=51430))
Many thanks to Thexter for his excellent work on this algorithm. Smoothswing V1 doesn't actually use any of the variables from the configuration file. The swingl and swingh files are played in a loop. The software will then place a rotating plane through the blade of your saber, and if the saber swings in one direction across the plane, we'll play more of swingl and less of the background hum. If we swing in the other direction, we'll play more of swingh and less of the hum. The fade will never blend swingl and swingh directly, it will essentially cross-fade between the regular hum and one of swingl/swingh based on direction and strength of the swing.

#### SmoothSwing V2
[Demo Video](https://www.youtube.com/watch?v=LHpzbtBo-5w) ([Thexter's description](http://therebelarmory.com/thread/9138/smoothswing-v2-algorithm-description))
Smoothswing V2 has some similarties to V1, but is much better at producing natural swing- and spin-like sounds, and also produces more variety than the V1 algorithm. To do this, the swinglNN.wav and swinghNN.wav files are paired up. Whenever a swing is not going on (swing speed < SwingStrengthThreshold) a new pair if selected randomly. As we start swinging, we keep track of how many degrees the saber has swung so far, and at a randomly selected threshold, we start a cross-fade to go from swingl to swingh. The transition lasts for Transition1Degrees, and if the swing continues, we will eventually cross-fade back from swingh to swingl 180 degrees after the first threshold. The second transition is generally wider and is controlled by Transition2Degrees. The combined swing sound is then cross-faded with the regular hum based on the swing strength.