---
title: The CONFIG_BUTTONS section
---
The CONFIG_BUTTONS is probably the simplest of all the sections in the config file. While it doesn't have to contain anything at all, it's purpose is to contain the buttons. The buttons are global variables in in C++, and we just create the variables directly in the config file. The general format looks like:

    TYPE Name(BUTTON, PIN, "name");

For buttons, the Name is not used, so it can be anything you like. (Well, anything that is allowed by C++ as least.)  The type, should be one of Button, LatchingButton, InvertedLatchingButton or TouchButton.

The BUTTON argument should be one of:

    BUTTON_POWER
    BUTTON_AUX
    BUTTON_AUX2
    BUTTON_UP
    BUTTON_DOWN
    BUTTON_LEFT
    BUTTON_RIGHT
    BUTTON_SELECT

Although most sabers only use the first three. This specifies what type of event this button will
generate when activated.

The PIN is the pad wired to the button. Most of the time it will be one of these symbolic names:

    powerButtonPin
    auxPin
    aux2Pin

These symbolic names are mapped to numbers by the proffieboard config file which is normally included in the CONFIG_TOP section.<br/>
Button pins, data pins and rx/tx pins could all be used as buttons.

The "name" is not very important, but is used to identify the button in error messages, top and commands.

For TouchButton, there is a fourth argument (a number), which must be tweaked to make the button work well.
To establish what value to use, use the serial monitor and type "monitor touch". Pay attention to the values printed out when touching and not touching the button, then choose a threshold value somewhere in between.

Simple two-button example:

    #ifdef CONFIG_BUTTONS
    Button PowerButton(BUTTON_POWER, powerButtonPin, "pow");
    Button AuxButton(BUTTON_AUX, auxPin, "aux");
    #endif

