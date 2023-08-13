---
title: Sub-sub sounds
---

This feature is new in ProffieOS 7.x

Normally, when you make a sound font effect, you will create more than one of each type of sound, and ProffieOS will select one of those randomly. However, more and more features are showing up which lets you actually select which of the random sounds to be played. Here is a brief list of those features:

* TrDoEffect
* Using effect.Select() from the prop
* sound pairing
* strength-based accent swings

When one of these features are used, the selection of sounds isn't random anymore. Most of the time, this is fine and intended, but sometimes it can be boring, because it will make things sound the same every time. For instance, if you enable strength-based accent swings, and you swing the saber the same each time, then the accent swing will also sound the same each time. To allow randomness back into the processes, sub-sub sounds adds another sub-directory of sounds.

Let's say we want to make our accent swings more random. To do that, we would create a folder structure like this in our font directory:
```txt
swng/01/000.wav
swng/01/001.wav
swng/01/002.wav
swng/02/000.wav
swng/02/001.wav
swng/02/002.wav
swng/03/000.wav
swng/03/001.wav
swng/03/002.wav
swng/04/000.wav
swng/04/001.wav
swng/04/002.wav
```

A few things to note:
1. The file numbers must have three digits and start with 000.wav
2. Each directory must have exactly the same number of wav files in it, or you will get "error in font directory".
3. The directory names follow the same rules as normal effects, so they can start at 01, and 1-8 digits
4. All the features listed above will see this as 4 different sounds (swng01-04). So with the strength-based accent swings example, this means 4 different strength levels, but with 3 varieties of sounds for each level.
5. Out of the three files in the sub-directories, ProffieOS will choose which one to play randomly.
