---
title: How to test a FET
---

[FETs](/glossary.html#fet) can sometimes get damaged by shorts. However, it can be difficult to test if they are working or not, because when they are not supposed to be on, they behave just like if they were broken. So let's discuss some ways to check if they are working or not.

First or all: It's not easy to test if a FET is working if nothing is connected to it. However, if something *is* connected to it, it's fairly easy.

## Method 1
Connect the blade, turn your proffieboard on and make sure the blade you want to test is supposed to be on. Now measure the voltage between BATT+ and the LED pad on the board. If it's working, the voltage should be 3+ volts. When the blade is supposed to be off, the voltage shuld be less than 0.1 volts. Note that errors in your config file could potentially throw off these measurements, as the FET might never really be turned on.

## Method 2
This method is particularly effective for [simple LED blades](/config/blades/simplebladeptr.html). Basically, you just take a small piece of wire and short the relevant LED pad to BATT-. If that makes the LED light up, then LED and it's wiring is obviously OK, meaning that if it doesn't light up when you turn your saber on, it must either be a programming problem or a broken FET.  This method can work with neopixels too, but if the neopixels don't light up, it might be because the data isn't working properly, so there are more possible causes.

Now, before you jump to conclusions, please make sure that your proffieboard programming is actually trying to turn the FET on. If you're not sure, I recommend measuring the gate voltage on the FET. Make sure your multimeter probe is pointy enough, and measure the voltage between the FET gate and GND.

<img src="/images/fet-gate.jpg" width=223 height=348 alt="fet gate illustration" />

When the gate is supposed to be on, this voltage is supposed to be 3.3v. When the gate is off, this voltage is supposed to be 0v.

If the gate voltage is right, but the FET doesn't turn on (as determined by Method 1/2 above) then the FET is definitely broken, and you should probably try [using a different LED pad](/howto/switch-fets.html), replace the FETs on the board, or replace the board.

