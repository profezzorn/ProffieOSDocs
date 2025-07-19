---
title: Sound Font config.ini configuration
redirect_from:
  - /config/sound-font-config.ini-configuration.html
---
This page explains the parameters that are available in a sound font's `config.ini` file, and provides an example file. For more information on how to create a ProffieOS compatible sound font, [click here](/sound/sound-font-configuration.html)

```ini
# Default config.ini

# This specifies how many milliseconds before the end of the "out" sound the hum
# starts to fade in. Default 100
humStart=100

# From ProffieOS 7.x, you can use ProffieOSHumDelay to specify how many milliseconds
# from the beginning of out.wav to start the hum. If both ProffieOSHumDelay and humStart
# are specified, then ProffieOSHumDelay is the one that will count.
# If not specified or set to -1, humStart will be used instead.
# Defaults to -1.
ProffieOSHumDelay=-1

# The volume of the hum sound. Can be 0-16, where 0 is muted.
# Default 15
volHum=15

# The volume of all effect sounds. Can be 0-16, where 0 is muted.
# Default 16
volEff=16

# How fast (degrees per second) we have to swing before a swing effect is
# triggered. Default 250.
ProffieOSSwingSpeedThreshold=250

# How much to bend the response curve between swing speed and swing volume.
# Can be 0.01 - 2.0, where value of 1.0 will result in no bending. Default 0.5
ProffieOSSwingVolumeSharpness=0.5

# The volume multiplier when swings are at the swing speed threshold.
# Can be 1.0 to 3.0. Default 2.0
ProffieOSMaxSwingVolume=2.0

# Specify what fraction of swing that must be played before a new swing can be
# started. Can be 0.0-1.0. Defaults to 0.5 (50%).
ProffieOSSwingOverlap=0.5

# This is used to control the volume of the combined hum and smoothswings
# when an accent swing plays.                       
# Defaults to 0.2 (volume is decreased by 20% of swing volume)    
ProffieOSSmoothSwingDucking=0.2 

# How slow (degrees per second) the swing has to be before it's not considered a
# swing anymore. Default 200.
ProffieOSSwingLowerThreshold=200

# Only used for non-smoothswing fonts. Specifies how aggressive a swing has to be to be considered a slash. Once we
# reach the ProffieOSSwingSpeedThreshold, rate of swing speed change is used to
# determine if it's a swing or a slash. Default 260
ProffieOSSlashAccelerationThreshold=260

# For OLED displays. This specifies the frame rate of animations.
# If not specified (or set to zero) the frame rate will be 24 frames
# per second for non-looped animations. For looped animations, the
# frame rate will be set so that the loop takes one second.
ProffieOSAnimationFrameRate=0.0

# For OLED displays, the time a blade style's "message", 
# static BMP, or loop animation will play when changing presets.
ProffieOSFontImageDuration=5000.0

# For OLED displays, the time an on.bmp will play
ProffieOSOnImageDuration=5000.0

# For OLED displays, the time a blst.bmp will play
ProffieOSBlastImageDuration=1000.0

# For OLED displays, the time a clsh.bmp will play
ProffieOSClashImageDuration=500.0

# For OLED displays, the time a force.bmp will play
ProffieOSForceImageDuration=1000.0

# If #define ENABLE_SPINS is defined. Number of degrees the blade must travel while staying above the
# swing threshold in order to trigger a spin sound.  Default is 360 or
# one full rotation.
ProffieOSSpinDegrees=360.0

### ---- These below as of OS6 only ---- ###

# Minimum acceleration for Accent Swing file Selection
#recommended value is 20.0 ~ 30.0
ProffieOSMinSwingAcceleration=20.0

# Maximum acceleration for Accent Swing file Selection
#must be higher than Min value to enable selection
#recommended value is 100.0 ~ 150.0
ProffieOSMaxSwingAcceleration=100.0

# Match sequential effects such as preon->out.wav files
# EFFECTNAME can be “preon”, “out”, “pstoff”, etc.
# Set to 1 *AND* have the same number of files in the second effect to activate this feature.
# ProffieOS.SFX.EFFECTNAME.paired=1
# For example:
# ProffieOS.SFX.preon.paired=1
# ProffieOS.SFX.out.paired=1
#
# Also, when multiple hum files exist, this will loop the 
# same hum sound until next ignition instead of randomly 
# choosing a different file once the current hum ends.
# ProffieOS.SFX.hum.paired=1

# Set the volume for each effect individually, in percent.
# 50 makes it half as loud. 200 makes it twice as loud. 
# Maximum allowed value is currently 255. The default is 100.
# EFFECTNAME can be "clash", “preon”, “out”, “pstoff”, etc.
# ProffieOS.SFX.EFFECTNAME.volume=100

### ---- OS 7.x and above ----

# Note, that from ProffieOS 7.x, all of the ImageDuration
# variables can be set to zero, in which case the length
# of the played wav file will be used to determing how long
# to show the image for.

# For OLED displays, the time a out.bmp will play
ProffieOSOutImageDuration=2000.0

# For OLED displays, the time a in.bmp will play
ProffieOSInImageDuration=2000.0

# For OLED displays, the time a pstoff.bmp will play
ProffieOSPstoffImageDuration=2000.0

# For OLED displays, the time a on.bmp will play
ProffieOSOnImageDuration=5000.0

# If true (non-zero) then smoothswing pairs will be played
# in sync with the hum. This means that you could have a
# musical beat in the hum, and smoothswing sounds could have
# melodies which would be played in sync with the beat.
ProffieOSSmoothSwingHumstart=0

### ---- OS 8.x and above ----

# Smoothswings default to switch back to the other sound again after 180 degrees.
# This 180 degrees is controllable by using the following:

#Low2HighSeparationDegrees=180

#High2LowSeparationDegrees=180

# How long it takes for the idle sound to fade in when
# it first starts playing. It loops at full volume afterwards.
# Default 3.0
ProffieOSIdleFadeIn=3.0
```

From ProffieOS 7.x forward, if there are multiple config.ini files in the font search path, they will all be read. Values specified in the first one will take precedence over values specified in the second one, and so forth. In ProffieOS 6.x and earlier, only once a config.ini was found, no more files were read.
