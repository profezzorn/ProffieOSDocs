If no other prop file has been set manually in the config file, then the default file gets used, which is the "saber.h" prop file, and this is how the buttons will work:
```
On/Off -                  Zero buttons saber = Twist (2 directional, like revving a motorcycle)
                          ** Note that the motion has to be done long enough to count, so a very quick flick of the wrist will not work.
                          1 button saber = Click to turn the saber on or off.
                          2 button saber = Click POW
                          ** Note, if #define DUAL_POWER_BUTTONS is added to config file,  Clicking either POW or AUX will power on.
                             Also note that POW and AUX become swapped while the saber is on if AUX used to power on.
Turn On muted -           Double-click POW button
Next preset -             Zero button saber = Point up and shake
                          1 or 2 button saber = Hold POW button and hit the blade while saber is off.
Previous Preset -         Hold AUX button and click the POW button while saber is off.
Clash -                   Hit the blade while saber is on.
Lockup -                  Hold either POW or AUX, then trigger a clash. Release button to end.
Drag -                    Hold either POW or AUX, then trigger a clash while pointing down. Release button to end.
Melt -                    Hold either POW or AUX and stab something.
Force Lightning Block -   Click AUX while holding POW.
Force -                   Long-click POW button.
Start Soundtrack -        Long-click the POW button while blade is off.
Blaster block -           Short-click AUX button.
Enter/Exit Color Change - 1 button saber = Hold button and Twist.
                          2 button saber = Hold Aux and click POW while on.
** Note Color Change only works with ProffieOS 3.x and above)
```

Note that other button configurations are available by using different prop files. Several prop files are already provided with ProffieOS and can be found in the [props directory](/profezzorn/ProffieOS/tree/master/props/). To learn how to use a different prop file, see the [The CONFIG_TOP section](The-CONFIG_TOP-section.md).