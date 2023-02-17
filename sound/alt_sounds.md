---
title: Alt Sounds
---

From ProffieOS 7.x, sound fonts can can have alternatives for some or all sound effects.

## File structure
Let's say we want to create a light and a dark version of the same font, and the only sounds we actually want to change to do that is the hum and the force sounds.

Before, our font directory looks like this: (some effects omitted for brevity.)
```txt
clsh/
font.wav
force/
hum.wav
in/
out/
swingl/
swingh/
```

The force directory then contains a number of files, like:
```txt
force/01.wav
force/02.wav
force/03.wav
```

Now, to set up this font with two alternatives, we create alt directories called alt000 and alt001. Alt directories must always have three digits and always start at 000. We then move the hum.wav and force directory into one of the alt directories, and we create a new hum and force for the other alt directory. Our top level directory thus looks like:

```txt
alt000/
alt001/
clsh/
font.wav
in/
out/
swingl/
swingh/
```

And the alt directories have the following content:
```txt
alt000/force/01.wav
alt000/force/02.wav
alt000/force/03.wav
alt000/hum.wav
alt001/force/01.wav
alt001/force/02.wav
alt001/force/03.wav
alt001/hum.wav
```

Note that alt001/force and alt002/force has the same number of files in it. This is important; every alt directory MUST have exactly the same set of files in them. Only the length and content of the files can be different. If you don't have the same set of files, you will get an "error in font directory" error.

## Controlling which alternative is used.
Ok, so now our has two sets of hum and force sounds, but how do we select which set of sounds is actually used? ProffieOS does not actually do anything to select which alternative is used by default, it just provides ways for you do it, either from a blade style, or from a prop. I will now describe a few ways that this could work, but it's by no means the only ways.

### SyncAltToVariance
By putting SyncAltToVarianceL or SyncAltToVarianceF in your style, which alt is used will be linked to the variance. This makes it super-easy to create blade styles which switch colors AND sounds at the same time. Any controls used to change the variance (color change) will also affect the alt sounds.

Example, here is a simple layered style:
```cpp
StylePtr<Layers<
  ColorChange<TrFade<300>,Red,Blue>,
  LockupL<AudioFlicker<Rainbow,White>>,
  SimpleClashL<White>,
  InOutHelperL<InOutFuncX<Int<300>,Int<800>>>>>()
```

SyncALtToVarianceL is an always-transparent layer, so we can basically insert it anywhwere in the layer stack, except at the beginning:

```cpp
StylePtr<Layers<
  ColorChange<TrFade<300>,Red,Blue>,
  SyncAltToVarianceL,
  LockupL<AudioFlicker<Rainbow,White>>,
  SimpleClashL<White>,
  InOutHelperL<InOutFuncX<Int<300>,Int<800>>>>>()
```

There, now alt and variance will be synchronized, so the Red color will play alt000 sounds and the Blue color will play alt001 sounds.

### TrDoEffect<EFFECT_ALT_SOUND, N>
By using TrDoEffect, with the EFFECT_ALT_SOUND effect, we can have the style explicitly select which alt sounds are used. This means that you can trigger alt sounds based on effecs and pulses. This creates the ability to move between states in the style, and you can check which state you are in by using the AltF<> function. The possibilities here are endless, but also more complicated, so I will leave it up to the reader to figure out good examples of how to use this.

### Have the prop control the alt.
If your prop has builtin modes, it might make sense to switch alt sounds when you switch mode as well. For fonts that don't have alt sounds, this will have no effect. A prop that wants to do this sould call SaberBase::DoEffect(EFFECT_ALT_SOUND, 0.0, N), which is basically the same as the TrDoEffect<> shown above. The prop could also control the variance, and let the style decide if the font should be synchronized with the variance or not. Doing it this way would essentially disable the "color change" functionality though.

