---
title: Serial Monitor Commands
redirect_from:
  - /serial-monitor-commands.html
---
This a list of some of the most typical commands you can use in the Serial Monitor.  
For more diagnostic/developer based commands, see [Serial Monitor Additional Commands](/tools/serial-monitor-additional-commands.html).   
The console can be opened in Arduino by choosing menu Tools>Serial Monitor.  
Type the command in the top box and hit return, or click the "Send" button on the right side.  
*Note* - Commands listed under the **Diagnostic Commands** section below only work if  
`#define DISABLE_DIAGNOSTIC_COMMANDS` in NOT active in the config.h file. 

## version

Prints which ProffieOS version is running.

## reset

Reboots the Proffieboard.

## RebootDFU

Reboots the Proffieboard as STM32BOOTLOADER device.

## get_volume

Displays the current volume.

## set_volume xxxx

Sets the current volume of the board. Overrides the value uploaded in your config.h file.

## n

Go to next preset.

## p

Go to the previous preset.

## on

Turn the saber on.

## off

Turn the saber off.

## clash

Trigger a clash

## force

Trigger a force push effect.

## blast

Trigger a blast effect.

## stab

Trigger a stab effect.

## lock

Begin/end lockup mode.

## lblock/lb

Begin/end lightning block.

## drag

Begin/end drag.

## melt

Begin/end melt.

## quote

Triggers quote.

## swing

Triggers swing/accent swing.

## slash

Triggers accent slash.

## spin

Triggers accent spin (if enabled with ENABLE_SPINS)

## ccmode

Enter/exit color change mode.

## cd <directory>

Use the specified font directory. Full path needs to be provided.

## pwd

Shows what font directory is currently active.
   
## dir <directory>

Show the contents of a directory on the SD card. Full path needs to be provided. 

## play <file>

Plays a particular file.

## play_track <file>

Like "play", but uses the track player to play it, which means that you can stop the track with "stop_track".

## stop_track

Stops the currently playing track, if any.

## scanid

Have the board deactivate all current blades, check the BladeID and pick a BladeConfig [] array based on the new detected BladeID.

## pow / aux / aux2 (or any button name)

These commands can be used to send button events from the Serial Monitor.
See [Button Commands](/button-commands.html) for more information.  

## blink N

Blink Status LED N times (Proffieboard V3 only)

# Editing Presets in Place (writes to presets.ini)
## rotate

Rotating is an alternative to saving the current preset. It puts the last preset first and saves presets.ini/tmp.

## list_presets

Prints currently programmed presets.

## set_font FONTNAME

Set current font.

## set_track (full path to)TRACK

Sets current track. 

## set_name NAME

Set current preset name.

## set_style

Set current style.  
  
<br/>
<br/>  

# Diagnostic Commands  
  *Note:* The uploaded config file can not have `#define DISABLE_DIAGNOSTIC_COMMANDS` active for these to work.

## beep

Plays a few beeps, great for testing if your speaker is working.

## dir

List contents of current font directory.

## effects

List all found effect sounds in font search path.

## sdtest

Tests the speed of the sd card. From ProffieOS 3.x and forward, this will read all the files in the current
font, then present an average speed and a histogram of how long it took to read each block and open each file.

## sdtest all

Like the "sdtest" command, but reads every file on the SD card, this can take a while.

