---
title: BlasterCharge
---

# Usage
```cpp
BlasterCharge
```

# Arguments
No arguments

# Description
Return 0-32768 based on the fullness of the clip / magazine.
Will cause compilation error if your prop doesn't have bullets.
You must define BLASTER_SHOTS_UNTIL_EMPTY for this to be available.
Recommended to be used as the EXTENSION argument to InOutHelperL.

# See Also
[BulletCount](/config/functions/BulletCount.html)

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/functions/bullet_count.h#L27
