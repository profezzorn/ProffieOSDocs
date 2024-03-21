---
title: Your first config file
---

Once you have Arduino installed and configured, it's time to download ProffieOS and set it up with a config file for your particular saber or prop. This page isn't meant to show you all the ways you can customize a config file, for now we're just going to start with something simple, and we can customize and configure it later.

## Where to get a config file.
While it's possible to just open up a text editor and write a config file, I wouldn't recommend it. Instead, I would go with one of these options:

* If you bought your saber from somewhere, the seller or installer usually saves the config file, or a copy of ProffieOS with a config file in it on the SD card. If you need help finding it, check [this page](/config/get-from-sd-card.html) Note that not all sellers/installers do this, and if that is the case, you should contact them and get the file directly from them.
* If you are installing your own Proffieboard, you can use the [configuration generator web page](/config/generator.html) to generate a config file for your board.
* You can take an existing, similar config file and modify it. (If necessary)
* You can use the [Fett263 configuration helper tool](https://www.fett263.com/fett263-os7-config-helper.html), but please beware that it requires you to input the blade configuration, so it's usually best to start with one of the other methods above, and then use the Fett263 tool to generate a *better* config file.
* There is also the [ProffieConfig tool](https://github.com/ryryog25/ProffieConfig), which aims to streamline this entire process, including uploads to the board.


## Configuring ProffieOS to use your config file.

1. Go to the ProffieOS directory and click on ProffieOS.ino (.ino might be hidden on Windows)
2. This should open up ProffieOS.ino in arduino. Arduino might show another file too, like README.md, if so, just click on the ProffieOS.ino tab.
3. Scroll down to the `CONFIG_FILE` define, it will be a line that looks like this:

```cpp
// #define CONFIG_FILE "config/YOUR_CONFIG_FILE_NAME_HERE.h"
```

4. Now change this line to:
```cpp
#define CONFIG_FILE "config/my_saber_config.h"
```
Of course, replace my_saber_config with the actual name of your config file.

