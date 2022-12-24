---
title: WavLen
---
## What is WavLen<>?  
WavLen (length of wav file) takes the duration of a wav file sound and can be used to replace time integer arguments in a blade style.   
For example, this is a simple InOutTrL that animates the ignition and retraction of the blade:
```
  InOutTrL<TrWipe<300>,TrWipeIn<500>>  
```
The retraction is currently set to WipeIn for 500 milliseconds.
Let's say you have an in.wav file that is 1000ms long.
As is, the blade retraction animation will reach the hilt and be "off" before the sound finishes. The sound and transition are out of sync.

If we tell WavLen to listen to the wav playing during retraction, it would look like this instead.
```
InOutTrL<TrWipe<300>,TrWipeInX<WavLen<EFFECT_RETRACTION>>>
```
Now, the animation of the WipeIn is timed to the total length of whichever wav gets chosen and stays in sync.
This is perfect for when there are various versions of in.wavs in a font, but they differ in duration.   
WavLen<> can be used in place of any Int<>, however it makes most sense to use it in a transition for one of the effect events so that there's actually a sound playing.

For a fade time of a clash for example:
```
ResponsiveClashL<White,TrInstant,TrFadeX<WavLen<EFFECT_CLASH>>,Int<26000>>,
```

## Syntax - Integer not number
Most transitions used in blade styles are aliased templates that have been shortcut to keep things a bit simpler.   
"Under the hood" though, they have an expanded syntax which needs to be understood a little to start substituting in WavLen for timings.   
TrFade<500> has 500 as a NUMBER.    
WavLen needs to replace an INTEGER.   
To expand TrFade<500> out to a format that takes an Int (so we can swap in WavLen)   
TrFade<> becomes TrFadeX<> and 500 Becaomes Int<500>, so it is now `TrFadeX<Int<500>>`   
It can be easy to forget there is now a new set of internal brackets around the Int<> value, so be sure to keep track of what you're writing.   
## Using WavLen in a TransitionEffectL   
When used inside a TransitionEffectL whose EFFECT is already specified at the end, WavLen<> will automatically use the right effect, so one does not need to be specified. This means it would be written as just `WavLen<>` like this:
```
TransitionEffectL<TrConcat<TrWipex<WavLen<>>,White,TrWipeX<WavLen<>>>,EFFECT_BLAST>
```

## Using Percentage<> with WavLen<>   
To use WavLen for an animation containing a chain of events in a TrConcat for example,
the time can be calculated and a Percentage of the wav can be used in each transition.
This force effect would fade in an unstable looking blade, then fade back out to reveal the base blade color again:
```
TransitionEffectL<TrConcat<TrFade<1000>,BrownNoiseFlicker<Red,Rgb<150,0,0>,500>,TrFade<1000>>,EFFECT_FORCE>
```
Since it's a 2 part effect, we can keep the half and half ratio of fade in/fade out equal to the sound duration time, even though the force.wav lengths may vary. In this case, we'd want each fade to take 1/2 the sound's duration. This is where Percentage gets applied.   
It gets wrapped around the WavLen, so in plain English it caould rad as "Get the percentage< of the <wav length of <the current force effect sound>> that is equal to 50"
```
TransitionEffectL<TrConcat<TrFadeX<Percentage<WavLen<>,50>>,BrownNoiseFlicker<Red,Rgb<150,0,0>,500>,TrFadeX<Percentage<WavLen<>,50>>>,EFFECT_FORCE>
```
Percentage can also be >100, so to have a transition take twice as long as the sound for example, the Percentage would be 200.

An expanded how-to video on this subject here: https://www.youtube.com/watch?v=5_Mn9KOyLb4