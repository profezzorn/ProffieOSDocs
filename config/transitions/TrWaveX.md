---
title: TrWaveX
---

# Usage
```cpp
TrWaveX<COLOR, FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER>
```

# Arguments
 * COLOR: COLOR
 * FADEOUT_MS, WAVE_SIZE, WAVE_MS, WAVE_CENTER: FUNCTION

# Description
TrWave is implements a wave traveling out from a specified point.
It's based on the Blast effect and is meant to look like a ripple starting
at a point on the blade. Unlike other transitions, this effect starts and ends
at the same color, and the wave is drawn using COLOR instead of the start/end
colors like most transitions do. It's intended to be used with TransitionLoopL
or TransitionEffectL, which take transitions that start and begin with the same
color.

# See Also
[TrSparkX](/config/transitions/TrSparkX.html), [Blast](/config/styles/Blast.html), [TransitionLoop](/config/styles/TransitionLoop.html), [TransitionEffect](/config/styles/TransitionEffect.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/transitions/wave.h#L4
