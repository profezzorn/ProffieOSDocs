---
title: Button Commands
---
The following instructions require `#define DISABLE_DIAGNOSTIC_COMMANDS` to NOT be enabled in the CONFIG_TOP section of the config file.

A config file typically uses "pow", "aux" and "aux2" as names for the available buttons, which means that those names can be used as commands from the Serial Monitor.

If you just type "pow", it will send an event which will match one of these cases in your prop file:

    case EVENTID(BUTTON_POWER, EVENT_CLICK_SHORT, MODE_OFF):
    case EVENTID(BUTTON_POWER, EVENT_CLICK_SHORT, MODE_ON):

(depending on whether the saber is on or off)

You can also specify which kind of click/hold/press/release event with the following shorthand:

* p = PRESSED
* r = RELEASED
* h = HELD
* m = HELD_MEDIUM
* l = HELD_LONG
* S = CLICK_SHORT
* s = SAVED_CLICK_SHORT
* L = CLICK_LONG

So if you type "pow L", it will match the following cases:

    case EVENTID(BUTTON_POWER, EVENT_CLICK_LONG, MODE_OFF):
    case EVENTID(BUTTON_POWER, EVENT_CLICK_LONG, MODE_ON):

You can also add a number to work with double/triple/quad-clicks. So for instance "pow s2" will match:

    case EVENTID(BUTTON_POWER, EVENT_SECOND_SAVED_CLICK_SHORT, MODE_OFF):
    case EVENTID(BUTTON_POWER, EVENT_SECOND_SAVED_CLICK_SHORT, MODE_ON):

Finally, these commands can also be used as modifiers for other commands. For instance, to execute a clash with the power button held, you'd type "pow clash", which would match a case like this:

    case EVENTID(BUTTON_NONE, EVENT_CLASH, MODE_ON | BUTTON_POWER):
    case EVENTID(BUTTON_NONE, EVENT_CLASH, MODE_OFF | BUTTON_POWER):

And a command like "pow aux" would match one of:

      case EVENTID(BUTTON_AUX, EVENT_CLICK_SHORT, MODE_ON | BUTTON_POWER):
      case EVENTID(BUTTON_AUX, EVENT_CLICK_SHORT, MODE_OFF | BUTTON_POWER):
