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
Next we must defines how many blades there are.
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

```cpp
#define VOLUME 1000
```

I don't remember why, but this next number is a constant instead of a define.
It specifies how many pixels we can have in a single strip. Note that if you use RGBW pixels, this number needs to be 25% bigger than your actual number of pixels. There is no need to make this smaller if your strips are not 144 pixels long, but you do need to make it bigger if they are more than 144 pixels long.

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
It's on my TODO list to make these not required:

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
For a visual reference for these, see [board_orientations.png](https://pod.hubbe.net/images/board_orientations.png)


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
DYNAMIC_BLADE_LENGTH
DYNAMIC_BLADE_DIMMING
DYNAMIC_CLASH_THRESHOLD
SAVE_VOLUME
SAVE_BLADE_DIMMING
SAVE_CLASH_THRESHOLD
SAVE_COLOR_CHANGE
*Note - `#define SAVE_STATE` is different, as that encompasses:
SAVE_VOLUME
SAVE_PRESET
SAVE_COLOR_CHANGE
SAVE_BLADE_DIMMING (From ProffieOS 7.9 onward)

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
