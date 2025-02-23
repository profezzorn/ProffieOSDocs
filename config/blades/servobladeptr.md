---
title: ServoBladePtr
---
ServoBladePtr takes 2 arguments, but usually you only have to specify one.

```cpp
    ServoBladePtr<PIN>()
// or
    ServoBladePtr<PIN, SELECTOR>()
```

The PIN argument is required and specifies which pin to use for the servo signal. Servo control signals are basic PWM signals at 50 hz. This is similar to SimpleBladePtr, except SimpleBladePtr uses 813 hz. The selector works similar to LED structs, but you probably don't need to mess with that for servos.
