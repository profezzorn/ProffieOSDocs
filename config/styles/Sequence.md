---
title: Sequence
---

# Usage
```cpp
Sequence&lt;COLOR1, COLOR2, int millis_per_bits, int bits, 0b0000000000000000, ....&gt;
```

# Arguments
COLOR1: COLOR
COLOR2: COLOR
millis_per_bit: millseconds spent on each bit
bits: number of bits before we loop around to the beginning
0b0000000000000000: 16-bit binary numbers containing the actual sequence.

# Description

Shows COLOR1 if the current bit in the sequence is 1, COLOR2 otherwise.
The number of 16-bit binary numbers should be at least |bits| / 16, rounded up.
Note that if not all bits are used within the 16-bit number.
Example, a red SOS pattern:
Sequence<RED, BLACK, 100, 37, 0b0001010100011100, 0b0111000111000101, 0b0100000000000000>

# Source Link
https://github.com/profezzorn/ProffieOS/blob/6f8add544c627172ad2dd698c90e5e55078a420a/styles/sequence.h#L4
