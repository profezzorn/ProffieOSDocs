Many people ask me: Do I need to hook up all those negative pads?

The answer is that you need to hook up at least two, and sometimes, you might want to hook up something like a switch or a connector between them.  If you know how electricity flow, just look at the circuit diagram and you can see why. However, if you don't know how electricity flows, here are a few simple rules:

There are two GND pads on the board, and you only need to hook up one of them.
You can use the other one(s) to hook up buttons, bluetooth modules or other things that needs GND, or it can be spliced into the wires, either way is fine.

Proffieboards also have two BATT- pads, and for the most part it's fine to hook up only one of them. The only reason there are two is to handle high current better. Hooking up both means less resistance, less heat and better cooling performance.

BATT- and GND must be connected together while the board is on. Normally this is done by just hooking them up together. However, sometimes BATT- is hooked up directly to the battery, while GND goes through a switch, charge port or blade connector. Hooking it up this way means that the switch/port/connector doesn't have to transmit the high current that goes through BATT-.  The board will automatically disable the FETs when GND is disconnected, which means that almost no current will leak through BATT- even though it is hooked up directly to the battery.

UPDATE: The pull-down resistors for the FET on TeensySaber and Proffieboards up to version 1.5 are hooked up to GND not BATT-, this means that the FETs will be left floating if GND is disconnected. Floating FETs can be either on or off or something in between, which is generally speaking not a good thing. If you disconnect GND on these boards, you must also disconnect BATT-, or the power to the LEDs. (Which is what happens if you use an 8-pin blade connector as shown in the wiring charts.)

