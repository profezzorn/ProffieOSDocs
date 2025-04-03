---
title: Restore Defaults
---

# Restore 'Factory' Defaults

If you have set SAVE-STATE, SAVE_VOLUME or any other save setting in your config, the system will save changes that you make to the system such as blade colour, preset etc. It does this by creating save files and storing them on the SD card. Deleting these files from the SD restores the system to 'factory defaults'. 
In the past, the only way to delete these files is by using a computer. However built in to the Sabersense button system is the facility to delete all save files simply with a button press.

This feature is enabled by default with the Sabersense prop File. If you wish to disable it, add this define to the CONFIG_TOP section of your config:

`#define SABERSENSE_DISABLE_RESET`
