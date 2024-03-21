---
title: Finding a config file on your SD card.
---

If your Proffieboard was configured for "Mass Storage" when configured, then you can connect a USB cable to your Proffieboard, and the contents of the SD card should show up on your computer, same as if you connected an USB drive. On windows, this would show up under "This PC" as a new drive.

If your board is not configured for "Mass Storage", then you will need to take the SD card out of the saber and use an SD card reader to access the files on the SD card. This may be preferable anyways since it is generally much faster than accessing the SD card through the Proffieboard.

When you open up the SD card, you should see something like this:

<image src="/config/images/sd_card_with_config.png" width=625 height=437 alt="sd card with config file" />

This SD card has a config file called "k4.h" in the root directory. Please note that depending on how windows is configured and what programs are installed, the ".h" part might not show, and it might just show an H in the `type` column instead. This can be very confusing, but unfortunately this is something windows does by default.

Unfortunatly, not everybody make it this easy to find the config file. Sometimes the config file in a sub-directory, in a zip file, and sometimes it will be a ".txt" file instead of a ".h" file. We'll talk about how to deal with that later.

Sometimes people put a zip file containing all of ProffieOS, with the config file on the SD card, like this:

<image src="/config/images/sd_card_with_proffieos.png" width=625 height=437 alt="sd card with proffieos" />

We could copy, unzip and use this directly, but since there is often a newer version of ProffieOS available, let's assume that we're only interested in getting the config file.

To do that, click on the zip file. Usually it contains a single folder called "ProffieOS-vX.Y", so click on that. In there there is usually a single folder called ProffieOS, so click on that. Now you should see multiple folders called blades, buttons, etc. Scroll down until you find a file called "ProffieOS", of type INO. (Or "ProffieOS.ino" if your windows installation shows extensions.) Now click on that. It should open up in Arduino (if you don't have Arduino installed, you can either install it, or use a text editor instead.)

Once the files open, scroll down until you see something like this:
<image src="/config/images/ino_with_config.png" width=611 height=464 alt="ProffieOS.ino with config file" />

Note that yours may look different, but only the lines WITHOUT // in the beginning counts. So in this case it shows that the config file we're looking for is called "k4.h" and it's in the "config" directory.

So we can close Arduino, then click on the "config" directory, and scroll until we find the file:

<image src="/config/images/config_in_config_directory.png" width=625 height=437 alt="config directory with config file" />

Once you find the config file, copy it to somewhere reasonable, like "Documents", or your desktop, and if need be, rename it to something that makes it easy to know which saber it's for.
