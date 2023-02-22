---
title: Pairing sequential effect sounds
---
Effect sounds in ProffieOS are played randomly when more than one file of a sound type exist (clsh01, clsh02, etc...)  
When using a polyphonic font, these can be triggered in succession and over lap each other, such as multiple blaster deflections.  
However, effect sounds that follow other sounds chronologically use a gapless transition as they are butted up to each other. An example of this is bgnlock->lock.  

These sounds can be paired so that the same number sound files play when the first sound is triggered.  
For example: preon01->out01, or bgndrag3->drag03.  
Let's say you have a Count Dooku sound font, and preon02 contain speech like  
"It is obvious that this contest can not be decided by our knowledge of The Force..."  
Wouldn't it be cool if the out.wav that followed had the ignition sound and included the rest of the sentence  
"...but by our skills with a Lightsaber." ? Well, as of ProffieOS6 that's possible.  
Or, if you have a few different hums in the font, and out03.wav works really well with one particular hum, then name that perfect hum hum03.wav and pair them up!  

## How to pair effect sounds
First, the same number of files must exist for each sound to be paired. (so 3 preon.wavs need 3 out.wavs.)  
If there are different amounts, pairing will be bypassed.  
Then, in the font config.ini file, an entry is made setting the ***first*** effect of the sequence to paired=1.   
For example:
```cpp
# pair preon -> out.wavs
ProffieOS.SFX.preon.paired=1
# pair in -> pstoff.wavs
ProffieOS.SFX.in.paired=1
```
As of ProffieOS7, we now have **all** of the sequential effects pairable, so possibilities include:  
preon->out  
out->hum  
hum->in  
in->pstoff  
bgnlock->lock  
lock->endlock  
*Note - this applies to all varities of lockup, so melt, drag, lb, arm  
 
```cpp
ProffieOS.SFX.hum.paired=1
```
When using this hum -> in pairing, the setting has another result.  
If multiple hum files exist, even if not the same number of files as in.wavs (so it won't pair to them,)  
this also will loop the same hum sound until next ignition instead of randomly choosing a different file once the current hum ends.  
