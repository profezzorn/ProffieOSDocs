---
title: Preset Configuration
---
In Proffie OS the term Preset means the combination of:
* Sound Font
* Music Track
* Blade Style
* A name for the preset

Presets are defined in object array of type _Preset_. A single Preset looks something like this:

    {
      "fontdir",
      "tracks/track.wav",
      style definition, // NUM_BLADES specifies how many style definitions there are
      "description",
    }

## Sound Font ("fontdir")
The first part of a preset is the directory of the sound font.
ProffieOS supports most of the major sound font formats that are widely used.
Sound-playing engine automatically detects through the files in the directory and switches to the appropriate mode.
* Plecter-style Fonts  (Including CFX style fonts, as of ProffieOS 3.x)
* Nec-styled Fonts
* Smooth Swing V1
* Smooth Swing V2

**Note**: Font directory should not exceed 8 characters

**Note**: Default sample rate in ProffieOS is 44kHz so all sounds with lower sample rates are upsampled automatically.

## Music Track ("tracks/track.wav")
In the second field is configured the audio track which can be used for soundtrack music or ambient sound in parallel to the rest of the sounds that are played by the saber.
Music Track invoke is configured to be runned via button combination or with Command send via the Serial port/Bluetooth module.

## Style definition
The style definition specifies the look and behavior of the blade itself. If more then one blade is used (NUM_BLADES is greater than 1) then more then one styles have to be defined in the current preset.

Style definitions, or "blade styles" are somewhat complicated, so they have their [own page](styles/blade-styles.html).

## Preset Description
The last element in a preset is the Preset Name. It is in the form of a character string, and while it is optional to include in the preset in order for it to compile, it is highly suggested to use since the preset name is used by [the ProffieOS workbench](../webusb.html) and OLED screens to identify the preset. Otherwise it will show nothing and you won't see what the preset is that you are working with.
Additionally, if there's a mismatch of number of styles per preset and the number of blades set, no helpful error occurs without the "name" argument in place.  
The preset description generally uses the [StarJedi](https://www.dafont.com/star-jedi.font) font when displayed.
As of ProffieOS 6, the name can be displayed on an OLED screen using an Aurebesh font by adding `#define USE_AUREBESH_FONT` to your CONFIG_TOP section.

