---
title: OnSpark
redirect_from:
  - /config/styles/OnSparX.html
  - /config/styles/OnSparL.html
---

# Usage
```cpp
OnSpark<BASE, SPARK_COLOR, MILLIS>
OnSparX<BASE, SPARK_COLOR, MILLI_CLASS>
OnSparL<SPARK_COLOR, MILLI_CLASS>
```

# Arguments
BASE: COLOR
SPARK_COLOR: COLOR (defaults to white)
MILLIS: a number (defaults to 200)
MILLI_CLASS: FUNCTION (defaults to Int<200>)
return value: COLOR

# Description
When you turn the saber on, it starts with SPARK_COLOR, and then
fades to BASE over a peariod of MILLIS millseconds.

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/on_spark.h#L4
