---
title: ResponsiveBlastFadeL
---

# Usage
```cpp
ResponsiveBlastFadeL<BLAST COLOR, SIZE, FADE, TOP, BOTTOM, EFFECT>
```

# Arguments
 * SIZE: controls blast size bump 0 ~ 32768
 * FADE: fade time ms
 * TOP: uppermost Blast position limit, BOTTOM = lowermost Blast position limit, 32768 = tip, 0 = hilt
 * EFFECT: effect type, defaults to EFFECT_BLAST

# Description
Implements Blast effect that will move based on angle of the blade instead of random location Blast will impact and Fade in position

# See Also
[ResponsiveLockupL](/config/styles/ResponsiveLockupL.html), [ResponsiveDragL](/config/styles/ResponsiveDragL.html), [ResponsiveMeltL](/config/styles/ResponsiveMeltL.html), [ResponsiveLightningBlockL](/config/styles/ResponsiveLightningBlockL.html), [ResponsiveClashL](/config/styles/ResponsiveClashL.html), [ResponsiveBlastL](/config/styles/ResponsiveBlastL.html), [ResponsiveBlastWaveL](/config/styles/ResponsiveBlastWaveL.html), [ResponsiveStabL](/config/styles/ResponsiveStabL.html), [Blast](/config/styles/Blast.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/responsive_styles.h#L154
