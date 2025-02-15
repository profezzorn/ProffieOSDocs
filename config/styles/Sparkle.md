---
title: Sparkle
redirect_from:
  - /config/styles/SparkleL.html
---

# Usage
```cpp
Sparkle&lt;BASE, SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY&gt;
SparkleL&lt;SPARKLE_COLOR, SPARK_CHANCE_PROMILLE, SPARK_INTENSITY&gt;
```

# Arguments
BASE: COLOR
SPARKLE_COLOR: COLOR (defaults to white)
SPARK_CHANCE_PROMILLE: a number
SPARK_INTENSITY: a number

# Description
Generally displays BASE, but creates little sparkles of SPARKLE_COLOR
SPARK_CHANCE_PROMILLE decides how often a spark is generated, defaults to 300 (30%)
SPARK_INTENSITY specifies how intens the spark is, defaults to 1024

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/sparkle.h#L4
