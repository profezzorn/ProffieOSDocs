---
title: Version Numbers
---

There has been some confusion about ProffieOS and Proffieboard version numbers, so I thought I'd write down how they are intended to work. 

# Version numbers are not decimal numbers
Version numbers are two separate numbers separated by a dot. This means that after 2.9 comes 2.10, and 2.25 is a much later version than 2.3. The first number is called the "major" version, and the second number is called the "minor" version.

# Versions are orthogonal
Think of as a street. As you go down the street, you see first avenue (version), then second avenue (version), etc. If you turn down one of the streets, you'll see version 1.1, 1.2, 1.3, etc. Unlike a city grid, there is no relation between the numbers on each street, so version 4.5 and version 6.5 have no connection in any way.  This also means that 3.0 does not follow the last version of the 2.x series. Instead it is most closely related to 1.0.

# Minor revisions are meant to be harmless
Only bugfixes are allowed when the minor version changes. So it should always be safe to upgrade to a later version of the same major version. (Like from 6.7 to 6.9) Only exception to this rule is in the beginning of the release cycle when we're still in alpha or beta stage.

# Proffieboards
Proffieboards also have versions, although it's much less obvious what they do since they rarely change.  Generally, when I design a new Proffieboard I start with a new major number, and every time I make some changes I change the minor version. Usually all of this happens before the board is ever released, which is why we get "1.5", "2.2" and "3.9" versions. However, if a problem/bug is found, we may see new revisions after the initial release.

# Versions are not releated.
Even though ProffieOS, Proffieboards and the Arduino-Proffieboard plugin all have similar version numbers, they can all mix or match. Just because you have a V3 proffieboard, doesn't mean you need to use version 3 of the Arduino-proffieboard plugin, or version 3 of ProffieOS.
