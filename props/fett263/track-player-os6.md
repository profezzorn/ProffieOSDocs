The Fett263 prop file (/props/saber_fett263_buttons.h) introduces a Track Player capability that allows unlimited tracks and 4 playback methods for ProffieOS6.

All presets should be set up as follows and a "common" folder should be added to the SD card with the Voice Prompts ([http://fredrik.hubbe.net/lightsaber/sound/](http://fredrik.hubbe.net/lightsaber/sound/))


***

{ "font;common", "font/tracks/trackname.wav",

StylePtr<...>(),

"preset name"

},

***

The default track in each preset should be set up the same as always, and all other tracks should be put in either "font/tracks/" if you want the tracks to be specific to a font/preset or "common/tracks/" if you want the tracks to be available universally for all presets.

Track files can be named anything so long as the entire string "font/tracks/trackname.wav" doesn't exceed 128 characters, although it's recommended to avoid spaces or special characters.  They do not need to be named sequentially but you can if it is easier to identify.

The Track Player looks in both the "font/tracks/" and "common/tracks" folder and if any track files are found they can be selected using the Dial menu.  If there are no wav files or "/tracks" is missing in both the font and common folder the default track will "Loop" in place of the Track Player.
After rotating through Tracks there are 4 playback methods:
* Play Once
* Loop - plays selected track on a loop until stopped
* Rotate - begins with selected track and rotates sequentially through each track until stopped
* Random - begins with selected track and randomly selects tracks until stopped

***

**Track Player Controls (2 Button) While Off**

    NEW! Track Player* = Long Click PWR parallel
      *requires tracks in either font/tracks/ or common/tracks/
      *if no tracks in font or common will "Loop" default track
      Turn Right (Stepped) = Next Track
      Turn Left (Stepped) = Previous Track
      Click PWR = Play Current Track Once
      Click AUX = Random (will play current track and then randomly select next tracks)
      Hold PWR + Turn Right = Rotate (will play current track and then next sequential tracks)
      Hold PWR + Turn Left = Loop Current Track
      Long Click PWR = Stop Track Player


***

**Track Player Controls (1 Button) While Off**

    NEW! Track Player* = Double Click PWR (parallel or down)
      *if only default track exists in current preset, track will "Loop"
      Turn Right (Stepped) = Next Track
      Turn Left (Stepped) = Previous Track
      Click PWR = Play Current Track Once
      Hold PWR = Random (will play current track and then randomly select next tracks)
      Hold PWR + Turn Right = Rotate (will play current track and then next sequential tracks)
      Hold PWR + Turn Left = Loop Current Track
