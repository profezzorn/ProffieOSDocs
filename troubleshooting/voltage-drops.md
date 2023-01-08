---
title: Finding Voltage Drops
---

Voltage drops can occur in any circuit, but the problem becomes more common the more current is going through the circuit. In a lightsaber, this generally means that all the components that provide power to the blade(s) may cause voltage drops. Depending on how severe they are, voltage drops can cause the blade to not light up, only show some colors (red) or become flickery or unreliable.  In partcular, only showing red colors is a very strong indication that voltage drops are occurring, so now it's just a matter of figuring out what is causing it.

Any component can cause voltage drops, this includes battery, wires, solder joints, connectors, charge ports, pogo pins, pogo pin PCBs, FETs, and anything else that is involved with transmitting or regulating the power. Fortunately, the procedure for finding where the problem occurs doesn't care what kind of component it is.

In most sabers, the power circuit looks something like this:

INSERT ILLUSTRATION HERE

1. Turn the saber on and ignite it with the blade connected.
2. Start at the battery, measure the voltage betweend + and -. Is it low? (Meaning less than 3.5 volts.) Then the battery is the problem. Try charging it. If that doesn't help, get a new battery.
3. Leave the negative probe on the battery -, and move the positive probe from + to the next step in the circuit. If the voltage changed by more than 0.1 volt, you have found a problem.
4. Once you reach the LED strip, the voltage *should* drop to near zero. If it doesn't, then the voltage drop is in the return path somewhere.
5. Keep moving the probe one step at a time, when the voltage drops down to ~0, then you have found a problem.

## Ok, so I found the problem, now what?

Well, it depends on what the problem is of course, here are a list of common voltage drop issues and what you can do about them:

### Bad / weak battery or battery protection circuit.
Get a new battery. You want a battery which is rated for at least 10A.

### Wires are too thin.
Use better wires. Minmum for saber wiring is AWG 24.

### Bad (cold) solder joints.
Usually this happens because the solder joints were not heated up enough, you should be able to fix it by just re-heating it, let the solder melt and then let it re-solidify.

### Shorts
Sometimes voltage drops happen because the power is shorted to another part of the circuit. The short will need to be fixed if that is the case.

### Insufficient FETs.
Some people only hook up a single FET (led pads) to power a blade. Sometimes that works ok, sometimes it doesn't. Use two or more FETs.

### Bad FETs.
FETs can become damaged if shorted. Check [the FET testing page](/troubleshoting/fet-testing.html) to learn how to check if they are working properly or not.

### Insufficient pogo pins
If you have a high-power blade, a 7-pin pogo pin adapter might not be sufficient, get one with 9 or 11 pins instead.

### Dirty / oxidized pogo pins or blade PCB
Try cleaning them. :)

### Voltage drops on the LED strip
Either you trimmed the LED strip too much, or you have a cheap strip with insufficient copper in it. Get new, better LED strips.

### Charge port voltage drops.
Make sure you have one that is rated for high amperes. Check that the spring contacts aren't bent back. If this doesn't help, replace it.

### Frayed wires
This tends to happen near solder joints, the copper strands break and only a few of them actually connect to the copper. Sometimes you need good magnification to see what is going on. If you have frayed wires, you'll have to cut, strip resolder or replace the wire.
