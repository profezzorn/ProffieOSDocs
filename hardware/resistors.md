---
title: Resistors
---
Proffieboard and TeensySabers wiring charts features three types of resistors:

## Current-limiting resistors

These are resistors used to limit how much current an LED receives. They can heat up and needs to be rated for enough watts to handle the. Values are usually in the 0.1-1ohm range, with watt ratings starting at 0.5 watts.
More about how to calculate the right values for these will be added later.

## Data-line resistors

These resistors are placed in-line on the data line for Neopixels. They are not always required, but help prevent the neopixels from sapping power from the data line. The power sap can be bad for the CPU and cause neopixels to glow even when they are supposed to be off. These resistors are generally in the 150-470 ohm range, and rated for 1/8th of a watt or more.

## Blade ID resistors

These resistors are used with replaceable blades to identify the blade. They are entirely optional. If you do use one, they are connected between the neopixel data line and GND. The board will test the Blade ID resistor and choose blade configuration and preset based on what it finds. Useful range is 2k to 100k ohm, watt ranting is pretty much irrelevant.

