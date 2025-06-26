---
title: DisplayStyle
---

# Usage
```cpp
DisplayStyle<MYDISPLAY>
```

# Arguments
 * MYDISPLAY: named instance
 * Returns: COLOR

# Description
This style requires a little more work than regular styles.
First you would need to declare an in-memory display.
To do this, we would put this in the CONFIG_STYLES section:

InMemoryDisplay<8, 8, 3> my_small_display;

Then you need a controller for it:

StandarColorDisplayController<8, 8> my_small_display_controller(&my_small_display);

Now we need give this display a name we can use in a style:

NAME_INSTANCE(my_small_display, MYDISPLAY);

Now we we can use this inside a style template:

DisplayStyle<MYDISPLAY>

Briefly, the display controller reads SCR files and tells
the in-memory display which PQF files to read. The PQF
files are rendered into an in-memory frame buffer.
DisplayStyle is used to read from that frame buffer.
Note that it's totally ok to use this with regular
blades, just make the height or the width of the
display equal to 1.

For more information about SCR files, read [the SCR Page](/display/SCR.html).  
For more information about PQF files, read [the PQF Page](/display/PQF.html).  
# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/display.h#L7
