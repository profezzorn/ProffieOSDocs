## BLADE_ID_SCAN_MILLIS

As of ProffieOS7, a new method of detecting different "blades" by using Blade ID is available.  
This can also include detecting other changes besides just blades, such as a removable chassis being inserted into a hilt.  
The following defines can be added to the config file:  

```cpp
#define BLADE_ID_SCAN_MILLIS 1000
#define BLADE_ID_TIMES 10
```
In the example above, 1000 is the milliseconds between scans, and 10 is the number of scans that get 
averaged together to come up with a useable scanned value.
These specific values have been tested to work well, but of course can be modified as desired.

Additionally, a BLADE_ID_CLASS will need to be defined, as well as SHARED_POWER_PINS for this method to work.  
See [Blade ID](blade-id.html) for more information.
