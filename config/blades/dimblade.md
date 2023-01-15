---
title: DimBlade
---
DimBlade is used to reduce the brightness of a blade, usually to save battery.

```cpp
DimBlade(percentage, blade_definition)
```

Note the use of () instead of <>, as DimBlade is a regular function, not a template. DimBlade will wrap a blade definition and reduce the brightness of the output. If percentage is 10.0, the blade will be 10% as bright, produce less heat and the battery will last longer. <br/>
Note that some effects, like clash will NOT be dimmed, which can make it stand out more than normal.<br/>
So for example, if you your blades array looks like this:

```cpp
BladeConfig blades[] = {
{ 0, WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(presets) },
};
```

Then here is how it would look with DimBlade():

```cpp
BladeConfig blades[] = {
{ 0, DimBlade(50.0, WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >()), 
CONFIGARRAY(presets) },
};
```

This would make your blade 50% as bright.
