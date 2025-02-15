---
title: AudioFlicker
redirect_from:
  - /config/styles/AudioFlickerL.html
---

# Usage
```cpp
AudioFlicker&lt;A, B&gt;
AudioFlickerL&lt;B&gt;
```

# Arguments
A, B: COLOR
return value: COLOR

# Description
Mixes between A and B based on audio. Quiet audio
means more A, loud audio means more B.
Based on a single sample instead of an average to make it flicker.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/audio_flicker.h#L4
