---
title: StringBladePtr
---
StringBladePtr is meant for old-style segmented blades and take 3 arguments, but only one is required:

    StringBladePtr<LED, clash_pin, clash_led>

* LED - led struct for the segments (see [LED configuration](led-configuration.html))
* clash_pin - pin that drives the clash string, if present, defaults to -1 (no clash string)
* clash_led - led struct for the clash string (see [LED configuration](led-configuration.html)) defaults to NoLED
