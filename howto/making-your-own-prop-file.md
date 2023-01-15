---
title: Making your own prop file
---
By default, the Proffieboard has a wide array of button actions, based on your config (1, 2, or 3 buttons.)  However, some of the default button actions can be less than ideal when spinning or dueling the saber.  For example, a simple short click on the power button will shut off the saber, which is easy to trigger by accident when handling the saber.  

So, how do we fix this?  Easy.

Button actions are handled by a prop file. The default prop file is called saber.h and can be found in the "ProffieOS/props/" directory. While you can modify saber.h directly, the recommended way is to make a copy of saber.h, then add the following to your config file:

```cpp
#ifdef CONFIG_PROP
#include "../props/yourfile.h"   // this assumes your copy is called "yourfile.h"
#endif
```

Inside the prop file, you'll find case statements that specify how buttons are handled. Case statements are a condition and an action, followed by "return true".  If the condition is met, then the action is triggered and the break stops other actions from firing in separate case statements.  Here's an example of the power off case statement from line 72 in props/saber.h:

```cpp
  case EVENTID(BUTTON_POWER, EVENT_CLICK_SHORT, MODE_ON):
  case EVENTID(BUTTON_POWER, EVENT_LATCH_OFF, MODE_ON):
  case EVENTID(BUTTON_AUX, EVENT_LATCH_OFF, MODE_ON):
  case EVENTID(BUTTON_AUX2, EVENT_LATCH_OFF, MODE_ON):
#if NUM_BUTTONS == 0
  case EVENTID(BUTTON_NONE, EVENT_TWIST, MODE_ON):
#endif
#ifndef DISABLE_COLOR_CHANGE
    if (SaberBase::GetColorChangeMode() != SaberBase::COLOR_CHANGE_MODE_NONE) {
      // Just exit color change mode.
      // Don't turn saber off.
      ToggleColorChangeMode();
      return true;
    }
#endif
    Off();
    return true;

  case EVENTID(BUTTON_POWER, EVENT_CLICK_LONG, MODE_ON):
    SaberBase::DoForce();
    return true;
```

So we see that there are four separate case statements that have the same action: Turn off color change mode and then call Off();  That Off() call turns off the saber, and can be triggered by the power button or aux button, depending on config (both momentary and latching.)  Most configs have two buttons: power and aux (both momentary), so we can ignore the three statements regarding latching switches.  

To alter the button behavior, we simply change
```cpp
  case EVENTID(BUTTON_POWER, EVENT_CLICK_SHORT, MODE_ON):
```
to
```cpp
  case EVENTID(BUTTON_POWER, EVENT_CLICK_LONG, MODE_ON):
```

Now a long press of the power button (any press longer than 500 ms) will shut off the saber when it's running.  However, this isn't the only change that needs to be made.  As you can see in the code, there is another action assigned to a long power button press while powered on: Force effects.  We need to 'move' this action because there can only be one case statement for a given button, condition and power state in the code, which means that two identical case statements will prevent the code from compiling and uploading to your saber.  In my case, I moved the Force effects from long press power to long press aux, like so:

```cpp
  case EVENTID(BUTTON_AUX, EVENT_CLICK_LONG, MODE_ON):
    SaberBase::DoForce();
    break;
```
Now we've changed power off to a long press and moved force effects to long press aux.  Hopefully this example shows how easy it is to change the case statements in the prop to customize your buttons to do exactly what you want them to do. 

To help further customize your preferences for button presses, the timings for different button events are as follows:

You get a EVENT_PRESSED event when the button is first pressed.<br />
If it was less than 500ms since the button was released, you also get an EVENT_DOUBLE_CLICK event.<br />
After 300ms you get an EVENT_HELD (If it's still held)<br />
After 800ms you get an EVENT_HELD_MEDIUM (If it's still held)<br />
After 2000ms you get an EVENT_HELD_LONG (If it's still held)<br />
Then, once the button is released you get: An EVENT_RELEASED event.<br />
If held <= 500 ms you get an EVENT_CLICK_SHORT<br />
If held > 500 and < 2500 you get an EVENT_CLICK_LONG<br />

Happy sabering!
