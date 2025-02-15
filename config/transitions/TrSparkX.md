---
title: TrSparkX
---

# Usage
```cpp
TrSparkX&lt; COLOR, SPARK_SIZE, SPARK_MS, SPARK_CENTER&gt;
```

# Arguments
COLOR: COLOR
SPARK_SIZE, SPARK_MS, SPARK_CENTER: FUNCTIONS

# Description
TrSparkX generates a wave without Fade over the length of the blade from
SPARK_CENTER. Unlike other transitions, this effect starts and ends
at the same color, and the wave is drawn using COLOR instead of the start/end
colors like most transitions do. It's intended to be used with TransitionLoopL
or TransitionEffectL, which take transitions that start and begin with the same
color.

# See Also
[TrWaveX](/config/transitions/TrWaveX.html), [TransitionLoop](/config/styles/TransitionLoop.html), [TransitionEffect](/config/styles/TransitionEffect.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/wave.h#L64
