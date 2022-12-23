StringBladePtr is meant for old-style segmented blades and take 3 arguments, but only one is required:

    StringBladePtr<LED, clash_pin, clash_led>

* LED - led struct for the segments (see [[LED configuration]])
* clash_pin - pin that drives the clash string, if present, defaults to -1 (no clash string)
* clash_led - led struct for the clash string (see [[LED configuration]]) defaults to NoLED
