---
title: The CONFIG_TOP section
---
The CONFIG_TOP section is primarily used to set up defines which enable and disable features in the code.
However, it is also used to include a board specific config file. Let's start with the required parts:

First, we must include a board config file, basically, we have to pick one of these lines:

```cpp
#include "v1_config.h"   // TeensySaber V1
#include "v2_config.h"   // TeensySaber V2
#include "v3_config.h"   // TeensySaber V3
#include "proffieboard_v1_config.h"  // Proffieboard V1
#include "proffieboard_v2_config.h"  // Proffieboard V2
#include "proffieboard_v3_config.h"  // Proffieboard V3
```

Note that if you include the proffieboard_config.h file (no version in the filename), the appropriate board version will be chosen for you based on which board is being programmed. This allows you to use your config on multiple versions of Proffieboards without needing to change this line to match.

### NUM_BLADES
Next we must define how many blades there are.
Note that accent LEDs, crystal chambers and light-up buttons also counts as blades.

```cpp
#define NUM_BLADES 1
```

### NUM_BUTTONS
And we must also specify how many buttons we have.
Note that this is just used to change how some of the buttons behave, and nothing will actually break if you specify a number different from your actual number of buttons.

```cpp
#define NUM_BUTTONS 2
```
### VOLUME
Then we specify the volumes. Generally values between 0 and 3000 are useful, but it may depend on what kind of board you have.  
To set the maximum volume of the saber, use this with the value of your choice:
```cpp
#define VOLUME 1000
```  
With some [prop files](/config/the-config_prop-section.html), you can use a volume menu to adjust the sound level of the saber. This menu's maximum volume is set by the above define.
Sometimes (like late night for example) you may want to boot the saber at a lower volume level, which can be adjusted up to the maximum later using volume menu. To do that, use this with the value of your choice:
```cpp
#define BOOT_VOLUME 300
```

### maxLedsPerStrip
I don't remember why, but this next number is a constant instead of a define.
It specifies how many pixels we can have in a single strip. There is no need to make this smaller if your strips are not 144 pixels long, but you do need to make it bigger if they are more than 144 pixels long.

```cpp
const unsigned int maxLedsPerStrip = 144;
```

### CLASH_THRESHOLD_G
Next, we have the clash threshold. When two consecutive accelerometer readings differ by this much, a clash is triggered. The unit is in Gs. (About 9.81 newtons.) Larger values will make clashes harder to trigger, smaller values will make clashes easier to trigger.

```cpp
#define CLASH_THRESHOLD_G 1.0
```

Please note that in ProffieOS 6.x, some changes were made to the motion detection system. This tended to make clash detection more sensetive, so it's not uncommon to have to increase the clash threshold when upgrading from 5.x to 6.x.

In ProffieOS 7.x, the clash detection was modified in ways that makes it less sensetive to false clashes. This change also means that the CLASH_THRESHOLD_G might have to be changed when upgrading from 6.x to 7.x. However, in this case you will probably be adjusting the clash threshold downwards rather than upwards.


Finally, we have a set of defines that enable standard features.
From ProffieOS 8.x, these defines are on by default and are not required.

```cpp
#define ENABLE_AUDIO
#define ENABLE_MOTION
#define ENABLE_WS2811
#define ENABLE_SD
```

# OPTIONAL defines

### ENABLE_SSD1306
This define enables the OLED display code.

```cpp
#define ENABLE_SSD1306
```

### OLED_FLIP_180
This code will flip the OLED displayed content 180 degrees.

```cpp
#define OLED_FLIP_180
```
### OLED_MIRRORED
Shows the OLED displayed content in reverse (for scopes that might use HUD 45 degree mirrors for example).

```cpp
#define OLED_MIRRORED
```
### PLI_OFF_TIME
Duration that the Power Level Indicator (battery level meter) will show on the OLED when blade is turned off.  
Example below show 10 seconds set.

```cpp
#define PLI_OFF_TIME 10000
```

### SHARED_POWER_PINS
This code makes it possible to use the same power pins for multiple blades.

```cpp
#define SHARED_POWER_PINS
```

### Orientation defines
If your board is installed in a different orientation than normal, you may need to add one of the following lines to make ProffieOS behave properly:

```cpp
#define ORIENTATION ORIENTATION_NORMAL  // USB connector points away from blade
#define ORIENTATION ORIENTATION_FETS_TOWARDS_BLADE
#define ORIENTATION ORIENTATION_USB_TOWARDS_BLADE
#define ORIENTATION ORIENTATION_USB_CCW_FROM_BLADE
#define ORIENTATION ORIENTATION_USB_CW_FROM_BLADE
#define ORIENTATION ORIENTATION_TOP_TOWARDS_BLADE
#define ORIENTATION ORIENTATION_BOTTOM_TOWARDS_BLADE
```
Here's a visual reference (viewed from above with the blade to the right):  
<img src="https://pod.hubbe.net/images/board_orientations.png" width=400 alt="board orientation_defines">


### ORIENTATION_ROTATION
For Curved hilts, or where the board is not parallel with the blade (for Twist on/off particularly)
This will rotate the orientation of the board 20 degrees around the Y axis.
Depending on the orientation of the board, you might need -20 degrees instead. (Or 15 degrees? or 30?)


```cpp
#define ORIENTATION_ROTATION 0,20,0
```

The values for the define are in degrees and in the order of `X,Y,Z`, the following image shows how these values translate to physical rotation of the board:
<img src="https://pod.hubbe.net/images/board_orientation_rotation.png" width=400 alt="orientation rotation">

### DUAL_POWER_BUTTONS
This one means that clicking the AUX will also turn the saber on.
If not defined, AUX will go to next preset when off.

```cpp
#define DUAL_POWER_BUTTONS
```

### ENABLE_SERIAL
This enables the serial port, which can be used to talk to a BLE chip.

```cpp
#define ENABLE_SERIAL
```

If you have a redbear BLE nano bluetooth chip, you'll need the following three defines to configure it:

```cpp
#define BLE_PASSWORD "password"
#define BLE_NAME "saber"
#define BLE_SHORTNAME "saber"
```

The BLE_PASSWORD must be 20 characters or less. BLE_SHORTNAME must be 8 characters or less.

### ENABLE_SERIALFLASH
This is only for TeensySaber V1 and enables the serialflash chip on the PJRC prop board

```cpp
#define ENABLE_SERIALFLASH
```

### ENABLE_FASTLED
This enables the FastLED blade driver, which can be used to drive dotstar blades.
This is experimental and may not work properly.

```cpp
#define ENABLE_FASTLED
```

### ENABLE_POWER_FOR_ID
To use blade ID in a 3-pin connector, the GND leg of the resistor has to be hooked up to the part that is controlled by FETs. That means that those FETs has to be powered on in order for blade ID to work. This define lets you do that by specifying which FETs needs to be powered while the blade is identified.

```cpp
#define ENABLE_POWER_FOR_ID PowerPINS<bladePowerPin1,bladePowerPin2,bladePowerPin3>
```

See [the blade ID page](../blade-id.html) for more information.

# ProffieOS 3.x defines

### ENABLE_DEVELOPER_COMMANDS
By default, some commands which are only useful for developers are normally not compiled into the final binary to save memory, if you want them, add this define to enable them.

```cpp
#define ENABLE_DEVELOPER_COMMANDS
```

Plase beware that this turns off some useful commands, like "sdtest" and "monitor".

### DISABLE_DIAGNOSTIC_COMMANDS
To save even more memory, you can disable some diagnostic commands like "monitor", "top" and "sdtest" using this define:

```cpp
#define DISABLE_DIAGNOSTIC_COMMANDS
```

### BLADE_ID_CLASS
Proffieboards have some challenges when it comes to BladeID, but it's possible to work around them by adding a bridge to another pin, or by adding a pullup resistor. However, when you do so, you have to use the BLADE_ID_CLASS to specify how the OS should calculate the Blade ID. Chose one of:

```cpp
#define BLADE_ID_CLASS BridgedPullupBladeID<bladeIdentifyPin, BRIDGED_PIN>
#define BLADE_ID_CLASS ExternalPullupBladeID<bladeIdentifyPin, PULLUP_RESISTANCE>
```

See [the blade ID page](/blade-id.html) for more information.

### IDLE_OFF_TIME
ProffieOS has pretty good standby idle time, but if you have accent LEDs that glow even when the saber is off, that will make your saber run out of batteries pretty fast. This define lets you specify a timeout for such accent LEDs (in milliseconds), this example would set it to 10 minutes:

```cpp
#define IDLE_OFF_TIME 60 * 10 * 1000
```

### DISABLE_COLOR_CHANGE
If you think color change is annoying, or you just need to save some memory, you can disable the color change feature with this define:

```cpp
#define DISABLE_COLOR_CHANGE
```

### BLADE_DETECT_PIN
This define lets you use a pin to detect when a blade is present or not. The pin will work kind of like a latching button which is pressed when there is a blade in the saber. When there is no blade in the saber, NO_BLADE (one billion) will be added to the blade ID.

```cpp
#define BLADE_DETECT_PIN PIN
```

See [the Blade Detect page](/blade-detect.html) for more information.

### SAVE_COLOR_CHANGE
On-the-fly color changing is new in 3.x. If you want it to save the color change state, add this define to your config file:

```cpp
#define SAVE_COLOR_CHANGE
```

### SAVE_VOLUME
Start with the volume used last

```cpp
#define SAVE_VOLUME
```

### SAVE_PRESET
Start at the last preset when you turn the saber on:

```cpp
#define SAVE_PRESET
```

### SAVE_STATE
Save state is one define to encompass SAVE_COLOR_CHANGE, SAVE_VOLUME and SAVE_PRESET. (From ProffieOS 7.8 onward, this also encompasses SAVE_BLADE_DIMMING)

```cpp
#define SAVE_STATE
```

# ProffieOS 4.x defines

### KEEP_SAVEFILES_WHEN_PROGRAMMING
From OS4.7 onward:
After uploading, all .INI file will be deleted from the SD card. These files may contain modifications to your uploaded config file such as saved colorcahngemode info, volume etc.
To retain this additional information even after re-flashing ProffieOS to the board, use:

```cpp
#define KEEP_SAVEFILES_WHEN_PROGRAMMING
```
    
Please use this define with caution. If you leave this define in your config file when you are tring to make changes to your saber, weird things tends to happen.

See [this page](/config/keeping-edits-when-uploading.html) for further information.

### ORIENTATION_ROTATION
If your board is not mounted at 90 degree angles to the hilt, you can use this define:

```cpp
#define ORIENTATION_ROTATION X,Y,Z
```

The X, Y and Z are floating point numbers which specify how many degrees to rotate all measurements.

# ProffieOS 5.x defines:

### RFID_SERIAL
Add an RFID reader. To configure the RFID reader, you will need an RFID_Commands array in [the CONFIG_PRESETS section](/config/the-config_presets-section.html).

```cpp
#define RFID_SERIAL Serial3
```

### SPEAK_TOUCH_VALUES
To calibrate your touch buttons, you can temporarily add this to your config to have ProffieOS say the touch values out loud. Can be confusing if you have more than one touch button. If you have more than one, calibrate one at a time and comment out the rest temporarily.

```cpp
#define SPEAK_TOUCH_VALUES
```

### ENABLE_I2S_OUT
This enables I2S output, Data3 is SCK, Data4 is FS and Button2/aux is DATA

```cpp
#define ENABLE_I2S_OUT
```

### ENABLE_SPDIF_OUT
This enables SPDIF output. The SPDIF signal will come out at 3.3 volts on Button2/AUX.

```cpp
#define ENABLE_SPDIF_OUT
```

### LINE_OUT_VOLUME
If you use ENABLE_I2S_OUT or ENABLE_SPDIF_OUT, you can control the volume with this define:

```cpp
#define LINE_OUT_VOLUME 2000
```

The default is 2000. If you want the line out volume to follow the master volume, you do:

```cpp
#define LINE_OUT_VOLUME dynamic_mixer.get_volume()
```

# ProffieOS 6.x defines:

Enables dynamic blade dimming / blade length / clash threshold, controllable from ProffieOS Workbench or some props.

```cpp
#define DYNAMIC_BLADE_DIMMING
#define DYNAMIC_BLADE_LENGTH
#define DYNAMIC_CLASH_THRESHOLD
```

Enable storing the dynamic dimming / clash threshold. Doesn't do anything unless the corresponding DYNAMIC_* define is also used.

```cpp
#define SAVE_BLADE_DIMMING
#define SAVE_CLASH_THRESHOLD
```

### INCLUDE_SSD1306
Includes support for ssd1306 displays, but does not automatically enable it. This lets you declare your own display and set the size and controller for the display.

```cpp
#define INCLUDE_SSD1306
```

### FILTER_CUTOFF_FREQUENCY
If present, these defines enable a butterworth highpass filter with the given order and cutoff frequency. The idea is to remove frequencies that your speaker can't reproduce anyways to put less stress on the speaker. The filter order defaults to 8. A reasonable cutoff frequncy might be 100Hz. The filter does not affect I2C or S/PDIF output if enabled.

```cpp
#define FILTER_CUTOFF_FREQUENCY
#define FILTER_ORDER
```

### NO_REPEAT_RANDOM
This define will make ProffieOS remember which file (of each effect) was played last and avoid playing it again next time. If there are only 2 of a particular sound, there is still a chance that the same sound is played to avoid simply flipping between them in a predictable pattern.

```cpp
#define NO_REPEAT_RANDOM
```

### FEMALE_TALKIE_VOICE
Uses a female talkie voice, only affects built-in error messages, for other sounds, go check out the Sound Library.

```cpp
#define FEMALE_TALKIE_VOICE
```

### DISABLE_BASIC_PARSER_STYLES
Saves memory by disabling old-fashioned styles. With this define, these styles will not be available in the ProffieOS Workbench.

```cpp
#define DISABLE_BASIC_PARSER_STYLES
```

### ENABLE_ALL_EDIT_OPTIONS
The following "umbrella" define is equivalent to separately defining:
* DYNAMIC_BLADE_LENGTH
* DYNAMIC_BLADE_DIMMING
* DYNAMIC_CLASH_THRESHOLD
* SAVE_VOLUME
* SAVE_BLADE_DIMMING
* SAVE_CLASH_THRESHOLD
* SAVE_COLOR_CHANGE
* MOUNT_SD_SETTING (from OS 8.x)

Note - `#define SAVE_STATE` is different, as that encompasses:
* SAVE_VOLUME
* SAVE_PRESET
* SAVE_COLOR_CHANGE
* SAVE_BLADE_DIMMING (From ProffieOS 7.9 onward)

```cpp
#define ENABLE_ALL_EDIT_OPTIONS
```

# ProffieOS 7.x defines

### BOOT_VOLUME	
Let's you specify what volume should be used at boot.  
Note that if `#define SAVE_VOLUME` is active (or SAVE_STATE or ENABLE_ALL_EDIT_OPTIONS since they also encompass SAVE_VOLUME), BOOT_VOLUME wil be overridden by your saved value.

```cpp
#define BOOT_VOLUME 300
```

### KILL_OLD_PLAYERS
When playing overlapping effects, you can sometimes run out of available wav players. When this define is enabled, ProffieOS will find the oldest playing overlapping effect and stop that sound to make room for the new sound to play. The result is that the new sound always plays.

```cpp
#define KILL_OLD_PLAYERS
```

### DISABLE_TALKIE
Saves 7.5kB of flash memory by disabling the spoken error codes that ProffieOS uses. The spoken error codes will be replaced with beeps, and you can use the ("What is it beeping?" page)[/troubleshooting/beep_codes.html] to figure out what the sounds mean. You can also see the errors in the (serial monitor)[/tools/serial-monitor.html].

```cpp
#define DISABLE_TALKIE
```

### BLADE_ID_TIMES
This define tells ProffieOS to run the blade ID multiple times and then average the results. This is particularly helpful when using BLADE_ID_SCAN_MILLIS, as the results tends to be very noisy otherwise.

```cpp
#define BLADE_ID_TIMES 10
```

### BLADE_ID_SCAN_MILLIS
With this define, blade ID will run all the time, even when the blade is on. The define specifies how many milliseconds in between each blade ID scan. Reasonable values might be 100 to 5000 ms. If the computed blade ID is different from the previous ones, then the saber will re-load blade definitions and presets, as if a Blade Detect event had occured.

```cpp
#define BLADE_ID_SCAN_MILLIS 500
```

Please note, you will most likely need BLADE_ID_TIMES and SHARED_POWER_PINS to use this define. Also, it currently only works with pixel blades.

### AUDIO_CLASH_SUPPRESSION_LEVEL

This define lets you adjust how much harder it is to do a clash when the audio is loud. The useful range is roughly 1 to 50, and the default is 10.

```cpp
#define AUDIO_CLASH_SUPPRESSION_LEVEL 20
```

### PROFFIEOS_DONT_USE_GYRO_FOR_CLASH

This define allows you to use only Accelerometer for Clash Detection (OS6 or earlier algorithm), instead of Accelerometer and Gyro combined (OS7 algorithm).

```cpp
#define PROFFIEOS_DONT_USE_GYRO_FOR_CLASH
```

### POV_INCLUDE_FILE

This define lets you include some other POV data instead of the default star wars logo. To learn how to generate pov data, go check out the [POV tools](/tools/pov.html)
```cpp
#define POV_INCLUDE_FILE "jedi_logo.h"
```
### BUTTON_DOUBLE_CLICK_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. It allows you to alter how many milliseconds can be between to clicks to make them count as a double click. The default is 500 milliseconds.
```cpp
#define BUTTON_DOUBLE_CLICK_TIMEOUT 500
```

### BUTTON_SHORT_CLICK_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. Pressing a button for a shorter than this counts as a "short click". The default is 500 milliseconds.
```cpp
#define BUTTON_SHORT_CLICK_TIMEOUT 500
```

### BUTTON_HELD_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. It determines how long after you press a button, the "held" event is fired. The default is 300 milliseconds.
```cpp
#define BUTTON_HELD_TIMEOUT 300
```

### BUTTON_HELD_MEDIUM_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. It determines how long after you press a button, the "held medium" event is fired. The default is 800 milliseconds.
```cpp
#define BUTTON_HELD_MEDIUM_TIMEOUT 800
```

### BUTTON_HELD_LONG_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. It determines how long after you press a button, the "held long" event is fired. The default is 2000 milliseconds.
```cpp
#define BUTTON_HELD_LONG_TIMEOUT 2000
```

# ProffieOS 8.x defines

### DISABLE_AUDIO
ENABLE_AUDIO is now the default, but this define can be used to disable it. This would only be used when developing support for new boards though.
```cpp
#define DISABLE_AUDIO
```

### DISABLE_MOTION
ENABLE_MOTION is now the default, but this define can be used to disable it. This would only be used when developing support for new boards though.
```cpp
#define DISABLE_MOTION
```

### DISABLE_WS2811
ENABLE_WS2811 is now the default, but this define can be used to disable it. This would only be used when developing support for new boards though.
```cpp
#define DISABLE_WS2811
```

### DISABLE_SD
ENABLE_SD is now the default, but this define can be used to disable it. This would only be used when developing support for new boards though.
```cpp
#define DISABLE_SD
```

### MOUNT_SD_SETTING
With this setting, you don't have to worry about your computer accessing the SD card and causing a corruption when you program the board anymore. By default, if you have "Mass Storage" selected in Arduino -> Tools -> USB Type, you can use access your SD card from you computer, basically, the Proffieboard performs the function of a (slow) SD card reader. Unfortunately, your computer may access the SD card when you don't expect it, and if interrupted at the wrong time, your SD card may become corrupt. This is why it is normally very important to "eject" the SD card before disconnecting or programming the proffieboard.

With MOUNT_SD_SETTING defined, ProffieOS will default to not allowing the computer to access the SD card, but you can change that setting at any time by using the comamnd "sd 1" in the serial monitor, an in-hilt menu setting, or by using the ProffieOS workbench. Then you can access the card like normal from the computer, and then make sure to "eject" it when you are done. Afterwards, you can use "sd 0" to disable access again. Note that the SD access setting is never saved and always returns to disallowing SD access when the saber is rebooted.

This setting is recommended for all users, especially when combined with a menu to enable/disable it easily.

```cpp
#define MOUNT_SD_SETTING
```

Note that MOUNT_SD_SETTING does not do anything unless you enable "mass storage" in Arduino.

### PROFFIEOS_LOG_LEVEL
This lets you quickly and easily control how much information ProffieOS will log to the serial monitor. 100 means only the absolute necesseties, 200 means include things that tell you what is going on, 300 is the default, which includes things you probably want to know, 400 is verbose logging, which includes things you don't normally need and 500 is spammy logging which includes lots of things that happen on a regular basis.
Higher values use more cpu and memory.
Lower values makes finding problems more difficult.
```cpp
#define PROFFIEOS_LOG_LEVEL 300
```

### DISABLE_NO_REPEAT_RANDOM
NO_REPEAT_RANDOM is on by default in ProffieOS 8.x, however, if you want to turn it off, you can still do so with this define.
```cpp
#define DISABLE_NO_REPEAT_RANDOM
```

### NO_BLADE_ID_RANGE
This define will change how blade ID works. Basically, if the blade ID is between the two given values, then the NO_BLADE (1 billion) will be added to the returned ID. The idea is that in most cases, the ID values returned when there is no blade in your hilt is different from when there is a blade in your hilt. By making ID values in that range return NO_BLADE, you may not need a blade detect pin to see if there is a blade in your hilt or not. This is particularly useful in combination with BLADE_ID_SCAN_MILLIS.

```cpp
#define NO_BLADE_ID_RANGE 100,1000
```

### MENU_SPEC_TEMPLATE
This define lets you specify what the "enter menu" button actually does. Currently there are two supported values:
 * DefaultMenuSpec - complete menu with settings, and edit mode menues
 * SettingsOnlyMenuSpec - limited menu with only settings
Note that this define is currently only supported by the saber.h and saber_BC_buttons.h prop. Other props will likely support this in the future.
```cpp
#define MENU_SPEC_TEMPLATE DefaultMenuSpec
```
You may also want to add the ENABLE_ALL_EDIT_OPTIONS define, or some menu entries might not be available.
To learn how to use the menus, see [this page](/howto/menus.html).

### MENU_SPEC_MENU
This define can be used together with MENU_SPEC_TEMPLATE to make the "enter menu" launch directly into a submenu. This means that only that submenu will be available, and all other menues will not possible to access. For instance, if you only want a volume menu, you could set this define to "ChangeVolumeMode". The name for each menu can be found in the menu specification.
```cpp
#define MENU_SPEC_MENU ChangeVolumeMode
```

### COLOR_MENU_GAMMA
ProffieOS uses linear colors, which means that Rgb<10,10,10> is exactly twice as bright as Rgb<5,5,5>, however, human visual perception is *not* linear, which means that it doesn't appear twice as bright. This is particularly apparent when using the menu system to adjust colors. The difference between Rgb<5,5,5> and Rgb<10,10,10> feels much more important than the difference between Rgb<205,205,205> and Rgb<210,210,210>. This is why computer RGB uses sRGB, which has a gamma of about 2.2. This define allows you to apply such a gamma factor when selecting R, G and B values in the color menus. A value between 2 and 3 will probably make the most sense. The higher the gamma value, the more space will be allocated to adjusting dark values, less space will be allocated for adjusting bright values. The default is 2.2, just like sRGB. You can try stting it to 1.0 to appreciate the difference. Note that some props have their own menus and might not use this define.

```cpp
#define COLOR_MENU_GAMMA 2.2
```
### CLASH_THRESHOLD_GAMMA
Just lke COLOR_MENU_GAMMA above, this only affects the clash threshold menu, and gives you more accuracy when adjusting low values than when adjusting high values. Default is 2.0. Note that some props have their own menus and might not use this define.

```cpp
#define CLASH_THRESHOLD_GAMMA 2.0
```

### VOLUME_MENU_GAMMA
Just lke COLOR_MENU_GAMMA above, this only affects the clash threshold menu, and gives you more accuracy when adjusting low values than when adjusting high values. Default is 2.2. Note that some props have their own menus and might not use this define.

```cpp
#define VOLUME_MENU_GAMMA 2.2
```

### BLADE_ID_SCAN_TIMEOUT
This define allows you to set a timeout on how long active
blade scanning will actually be active for. Similar to IDLE_OFF_TIME, but
just for the continous blade ID scan.

```cpp
#define BLADE_ID_SCAN_TIMEOUT 5 * 60 * 1000
```

### BLADE_ID_STOP_SCAN_WHEN_IGNITED
This define stops ID scanning while the saber is ignited. With no scanning there is no chance of getting the ID wrong and re-initialize the saber while using it.

```cpp
#define BLADE_ID_STOP_SCAN_WHEN_IGNITED
```

### ENABLE_SPIDISPLAY
Currently, including support for color displays use a small amount of memory even if no display is actually used. To work around this issue, we have this define. Without it, color display support is disabled and takes no memory. With it, you can use color displays in your config file.

```cpp
#define ENABLE_SPIDISPLAY
```

### FONT_PATTERN
When using the MENU_SPEC_TEMPLATE, you can edit and modify presets using menus. However, font packs are typically stored in a directory called `"common"`, so the font search path for each preset is typically on the form "font_directory;common". This works well in many cases, but can be somewhat limiting. By using this define, you can change the pattern used to extract and construct font search paths.  The default FONT_PATTERN is `"*;common"`, and the star is where the font directory will go. However, you could set it to something like `"override;*;common"`, and now any sound you put in `"override"` will be used by all fonts. There can also be multiple stars in the pattern, for instance, you could use `"*;*/mysaber;common"`, and if your font direcory is `"ANH"`, then the final search path will be `"ANH;ANH/mysaber;common"`. Note that, in order for ProffieOS to be able to extract the font directory from the font search path, all presets in your config file must have font search paths that match the pattern.

```cpp
#define FONT_PATTERN "*;common"
```

### SMOOTH_COLORCHANGE_TICKS_PER_REVOLUTION
This define enables "tick" sounds when using the smooth color change menu. The ticks don't actually have any meaning, but improves the feel of using the smooth color change menu nontheless. The define also specifies how many ticks to play per revolution.
```cpp
#define SMOOTH_COLORCHANGE_TICKS_PER_REVOLUTION 60
```

### ENABLE_IDLE_SOUND
This enables a sound effect called "idle", which is basically the inverse of "hum" as it will play when the saber is off, instead of when it's on. It will stop playing after IDLE_OFF_TIME has passed.
```cpp
#define ENABLE_IDLE_SOUND
```

### BUTTON_LONG_CLICK_TIMEOUT
This define is really meant to be used by a prop file, but can also be set in a config file. It allows you to alter the maxium time for a "long click". The default is 2500 milliseconds.
```cpp
#define BUTTON_LONG_CLICK_TIMEOUT 2500
```

