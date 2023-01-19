---
title: Your first ProffieOS installation
---

If you haven't already, make sure to do [the required setup steps](/proffieboard-setup.html) first.

## Download ProffieOS

1. Go to [the ProffieOS homepage](https://fredrik.hubbe.net/lightsaber/proffieos.html) and hit the download link.
2. Put it somewhere handy and unzip it.

You should now have a directory called ProffieOS with the following files in it:
```
Arduino.mk    ir/              README.md
blades/       LICENCE.txt      scripts/
buttons/      Makefile         sound/
common/       motion/          styles/
Common.mk     mtp/             Teensy.mk
config/       pov_tools/       transitions/
display/      Proffieboard.mk  videotoblc/
fontconvert/  ProffieOS.ino
functions/    props/
```

Note that Windows may hide the part after the period, so it may look a little different, but it's still the same files.

## The Config File

If you are upgrading an existing saber, then you may already have a config file, in which case, just use that. If you need to create a new config file, keep reading.

1. Go to the configurator page that matches your board:
  * Proffieboard V1.x: https://fredrik.hubbe.net/lightsaber/v4/
  * Proffieboard V2.x: https://fredrik.hubbe.net/lightsaber/v5/
2. Change the options to match how your saber is wired.
4. Go back to your ProffieOS directory, then into config/.
5. Make a copy of the file called `default_proffieboard_config.h`.
6. Rename the copy to something reasonable for your saber, like maybe `my_saber_config.h`. (Please note, that on Windows, the `.h`. is normally not shown. If it wasn't before you selected rename, don't add it.)
7. Open up the renamed file in a text editor. You can use Notepad, Notepad++, Sublime or any other editor that knows how to edit plain text. Do not use word, wordpad or other programs intended to edit documents. Documents and text are not the same thing.
8. Select all the contents in the renamed file and delete it.
9. Go back to the configurator page, scroll down and press the "copy to clipboard" button.
10. Paste it into the editor and save.

Congratulations, you now have a config file.

## Tell ProfffieOS to use your config file

1. Go to the ProffieOS directory and click on ProffieOS.ino (.ino might be hidden on Windows)
2. This should open up ProffieOS.ino in arduino. Arduino might show another file too, like README.md, if so, just click on the ProffieOS.ino tab.
3. Find the CONFIG_FILE define, it will be a line that looks like this:

```cpp
// #define CONFIG_FILE "config/YOUR_CONFIG_FILE_NAME_HERE.h"
```

4. Now change this line to:
```cpp
#define CONFIG_FILE "config/my_saber_config.h"
```

Of course, if you used a different filename in the previous step, use that filename instead of `my_saber_config.h`.

## Upload

1. Connect your board to the computer using an micro-usb cable. (Make sure it's not a charge-only cable.)
2. In Arduino -> Tools -> Port, make sure that the board shows up and is selected as the current port. If this doesn't work, see [this page](/troubleshooting/wheres-my-port.html).
3. If the Proffieboard shows up as a drive on your computer, make sure to "safely remove" it before uploading the board.
4. Press the upload button.

Check out what happens in the window at the bottom of Arduino. You may need to scroll around to see what's going on. You can also make the window bigger, which helps. If you see a 0-100 progress bar and it goes all the way to 100, then the programming worked, regardless of what other errors and warnings you see.

Now your saber is programmed. You can tweak your config file as many times as you like and re-upload as many times as you like.
