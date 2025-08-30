---
title: SD Card troubleshooting
---

SD card problems is probably the most common issue with Proffieboard setups. ProffieOS uses SD cards in an unusual way, which puts high high demands on the SD cards in ways that they are not always well optimized for. Also, all SD cards will go bad sooner or later. It's not a matter of IF, it's a matter of WHEN.

# How does SD cards work?
Fundamentally, SD cards are flash storage devices. They shoot electrons into little traps and keep them there, that's how they store the actual information. The reliability of these cells depends on how big they are. Bigger cells are more reliable, but also more costly, so naturally SD card manufacturers want to keep the cells as small as possible. Cells also also wear out eventually. The electron bombardment actually wear down the cell walls over time, making the cells less reliable.

To work around this, SD cards have a cpu, and use a variety of strategies to make these cells more reliable, these strategies include, but are not limited to:
 * using checksums to detect when data is not read back correctly
 * using CRC to automatically fix data when it is not read back correctly
 * wear-leveling - SD cards usually have a table made of big reliable cells which specifies where each block is stored, and each time you write a block it will most likely be stored in a new location.
 * avoid-lists - blocks that require CRC or fail checksums repeatedly are added to a list and avoided. SD cards usually have some extra blocks that they can use when blocks go bad. How much extra basically determines the lifetime of the SD card.

If you've heard of these strategies before, it's because they are not new. Hard drives, CD roms and just about every storage device use these strategies to improve function.

So why am I telling you all this? It's because I want you to understand that things go wrong in SD cards *all the time*, but mostly it's hidden by some algorithm that improves the relibility. However, that algorithm may require some time to run, and that's not good for ProffieOS.  ProffieOS have has very small audio buffers. Basically only one 512-byte block, which at 16-bit 44100Hz is only about 11ms. That means that if a block read takes more than 11ms, there will be a gap in the audio. Since we may be playing multiple sounds, the limits are actually even less than that. To make matters even worse, opening a new file requires several block reads, and those must also finish within 11ms, or we get an audio underflow.  Typically, block reads take ~0.2-0.3ms, so we should have plenty of time, but because of the strategies employed by the card to hide minor errors, that's not always the case.

For the most part, SD cards are not really designed for low-latency reads. Most cards take the approach that 99.99% of all reads will be fast, and every now and then some block will take more time, and that's fine. If you were just copying photos to/from the SD card, who cares if one of the pictures takes 100ms extra to copy, right?  ProffieOS does, and now you do too.

So what can we do? Well, it might be helpful to look at the "A" rating for sd cards. The A rating is really about how many "transactions" the card can do per second. That's not exactly the same thing as reliably low latency, but it's at least more similar than the "U" rating which is based on the maximum possible throughput. The other thing I do is to look for "industrial" and "professional" cards, which may have bigger cells, more extra blocks and better CRC algorithms to improve reliability.  (No guarantees, they might also be the same cards with different print on them, I have no way of knowing.)

I also highly recommend using V3 cards which has higher SD card bandwidth, which makes it a little more tolerant to some of these kinds of problems.

# Clues

So what actually happens when SD cards go bad?
* reading certain parts of the SD card may be slow
* reading certain parts of the SD card may hang forever
* files and folders may be corrupted (this can also happen for other reasons, such as disconnecting prematurely.)
But what actually happens to ProffieOS in these cases?

# If SD card is slow
* Audio pops and glitches
* Audio underflow error messages in serial monitor
* Blade animations may freeze for short periods of time
* ProffieOS may freeze. This happens because playing audio is a high priority task for ProffieOS, and if the SD card is slow, playing audio may leave no time to do anything else.

# If SD card hangs forever
* ProffieOS will freeze, most likely producing a squee-of-death (if audio is playing when it freezes)

# If SD card is corrupt
* Sounds will not play.
* ProffieOS *may* crash
* Usually there are weird error messages in serial monitor which may end up looking like they are in a different language or something.
* Almost anything could happen.

# Tests

So, if you see some of these problems listed above, how do you know if it's the SD card or something else? Most of the time, the answer is to use the "sdtest" command in the serial monitor.

Please note that the "sdtest" command is not available if you have the DISABLE_DIAGNOSTIC_COMMANDS in your config file. If you have that in your config file, you will need to temporarily comment it out (by adding // in front of it) and upload to the board before you can run "sdtest". You may also need to temporarily comment out some presets from your config file to make everything fit in flash memory.

To run "sdtest" pull up the Serial Monitor in arduino, type in "sdtest" and press enter. You should see something like this:

```
Playing common/mnum/mnum1.wav

Playing common/mnum/mnum2.wav

Playing common/mnum/mnum3.wav

Playing common/mnum/mnum4.wav

Playing common/mnum/mnum5.wav

Playing common/mnum/mnum6.wav

Playing common/mnum/mnum7.wav

Playing common/mnum/mnum8.wav

Playing common/mnum/mnum9.wav
N
Playing common/mnum/mnum10.wav

Playing common/mnum/mnum11.wav
M
Playing common/mnum/mnum12.wav

Playing common/mnum/mnum13.wav
M
Playing common/mnum/mnum14.wav
M
Playing common/mnum/mnum15.wav
M
Playing common/mnum/mnum16.wav
M
Playing common/mnum/mnum17.wav
L
Playing common/mnum/mnum18.wav
M
Playing common/mnum/mnum19.wav
N
Playing common/mnum/mnum20.wav
M
Playing common/medit.wav
ML
Playing common/vmend.wav
NL
Playing common/vmbegin.wav
NL
Playing Rescue/endlb/endlb1.wav
K
Playing Rescue/endlb/endlb2.wav
M
Playing Rescue/endlb/endlb3.wav
M
Playing Rescue/lb/lb.wav
LKMLKLLLLLKMMKKMLLLKLMLKLK
Playing Rescue/bgnlb/bgnlb1.wav
L
Playing Rescue/bgnlb/bgnlb2.wav
L
Playing Rescue/bgnlb/bgnlb3.wav
NM
Playing Rescue/endmelt/endmelt.wav
L
Playing Rescue/melt/melt.wav
LLKLLKLLKLLKLLKLLLLKLMKKLLLLKK
Playing Rescue/bgnmelt/bgnmelt.wav
LMK
Playing Rescue/enddrag/enddrag1.wav

Playing Rescue/enddrag/enddrag2.wav
N
Playing Rescue/enddrag/enddrag3.wav

Playing Rescue/enddrag/enddrag4.wav

Playing Rescue/drag/drag.wav
LKLMLLLLLMKLM
Playing Rescue/bgndrag/bgndrag1.wav

Playing Rescue/bgndrag/bgndrag2.wav

Playing Rescue/bgndrag/bgndrag3.wav

Playing Rescue/bgndrag/bgndrag4.wav
Playing Rescue/swingh/swingh01.wav
NLLKLLKLLKLLKKMLML
Playing Rescue/swingh/swingh02.wav
NMMKLLKLLKMMK
Playing Rescue/swingh/swingh03.wav
MMLLLKLLKLLKLLKLLKLLK
Playing Rescue/swingh/swingh04.wav
MKLMLLLKLMKLMLLLLLLKLM
Playing Rescue/swingl/swingl01.wav
LLKLMLKLLLLK
Playing Rescue/swingl/swingl02.wav
MKLKLMLKLKKLKLMLLLLL
Playing Rescue/swingl/swingl03.wav
MMLLLKLLKKLKLLKMLLKLLK
Playing Rescue/swingl/swingl04.wav
LKLKKLMLKLLLLKLMLLK
Playing Rescue/swng/swng01.wav
L
Playing Rescue/swng/swng02.wav
M
Playing Rescue/swng/swng03.wav
M
Playing Rescue/swng/swng04.wav
N
Playing Rescue/swng/swng05.wav
M
Playing Rescue/swng/swng06.wav

Playing Rescue/swng/swng07.wav
M
Playing Rescue/swng/swng08.wav
N
Playing Rescue/swng/swng09.wav
N
Playing Rescue/swng/swng10.wav
M
Playing Rescue/swng/swng11.wav

Playing Rescue/swng/swng12.wav

Playing Rescue/swng/swng13.wav

Playing Rescue/swng/swng14.wav
M
Playing Rescue/swng/swng15.wav
M
Playing Rescue/swng/swng16.wav
M
Playing Rescue/lock/lock01.wav
LKLLKLLLMMKLLKLLKLLKLLKLLKLLKMM
Playing Rescue/out/out01.wav
LL
Playing Rescue/out/out02.wav
MM
Playing Rescue/out/out03.wav
MK
Playing Rescue/out/out04.wav
NL
Playing Rescue/in/in01.wav
L
Playing Rescue/in/in02.wav
M
Playing Rescue/clsh/clsh01.wav
L
Playing Rescue/clsh/clsh02.wav
N
Playing Rescue/clsh/clsh03.wav
N
Playing Rescue/clsh/clsh04.wav
L
Playing Rescue/clsh/clsh05.wav
N
Playing Rescue/clsh/clsh06.wav
N
Playing Rescue/clsh/clsh07.wav
M
Playing Rescue/clsh/clsh08.wav
M
Playing Rescue/clsh/clsh09.wav
M
Playing Rescue/clsh/clsh10.wav
M
Playing Rescue/clsh/clsh11.wav
M
Playing Rescue/clsh/clsh12.wav
M
Playing Rescue/clsh/clsh13.wav
ML
Playing Rescue/clsh/clsh14.wav
M
Playing Rescue/clsh/clsh15.wav
ML
Playing Rescue/clsh/clsh16.wav
MK
Playing Rescue/blst/blst01.wav
LL
Playing Rescue/blst/blst02.wav
M
Playing Rescue/blst/blst03.wav
ML
Playing Rescue/blst/blst04.wav
NM
Playing Rescue/blst/blst05.wav
M
Playing Rescue/blst/blst06.wav
MK
Playing Rescue/endlock/endlock1.wav
L
Playing Rescue/endlock/endlock2.wav
NL
Playing Rescue/endlock/endlock3.wav
ML
Playing Rescue/endlock/endlock4.wav
N
Playing Rescue/bgnlock/bgnlock1.wav
KL
Playing Rescue/bgnlock/bgnlock2.wav
NL
Playing Rescue/bgnlock/bgnlock3.wav
M
Playing Rescue/bgnlock/bgnlock4.wav
M
Playing Rescue/font/font.wav
KLLLL
Playing Rescue/stab/stab1.wav
LM
Playing Rescue/stab/stab2.wav
M
Playing Rescue/stab/stab3.wav
NM
Playing Rescue/stab/stab4.wav
NK
Playing Rescue/force/force1.wav
KLLKL
Playing Rescue/force/force2.wav
MKLLK
Playing Rescue/force/force3.wav
MMLLL
Playing Rescue/force/force4.wav
O
Playing Rescue/force/force5.wav
MKKLKLM
Playing Rescue/force/force6.wav
MK
Playing Rescue/force/force7.wav
NLK
Playing Rescue/force/force8.wav
NML
Playing Rescue/force/force9.wav
NLKLLLMKKLLK
Playing Rescue/hum/hum01.wav
MKLLKLLKMMKLMLLLNMLKMMKLLLLLLMLKMMKLMLLLKLL
Playing Rescue/boot/boot.wav
MLLLKLLK
Time to open files: Average time: 2561.39 us
                                             .  .                                                   
                                             :  :                                                   
                                             :  ::.                                                 
                                           . :  :::                                                 
                                           :::  :::                                                 
                                           :::  :::                                                 
                                           :::  :::                                                 
                                           :::..:::                   .                             
                                          .:::::::::                ::: .                           
                                          ::::::::::    .          .::: :                           
                           :              :::::::::: : :::         :::: :: :                        
x100us              1                   2                   3                   4                   5
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0
Time to read blocks: Average speed: 1924.88 kb/s, 21.82 simultaneous audio streams.
                                                                                                    
     :                                                                                              
     :                                                                                              
     :                                                                                              
     :                                                                                              
     :                                                                                              
     :                                                                                              
    .:                                                                                              
    ::                                                                                              
    ::                                                                                              
   .::.....                                                                                         
x100us              1                   2                   3                   4                   5
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0
Unmounting SD Card.
```

Here is what all of it means:

First of all, while it's running you see things like this:

```
Playing Rescue/hum/hum01.wav
MKLLKLLKMMKLMLLLNMLKMMKLLLLLLMLKMMKLMLLLKLL
```
What this means is that ProffieOS opened up the file "Rescue/hum/hum01.wav" and read it. For every 64kb, it writes out a letter which specifies how fast it was able to read it. If the speed is equivialent to one audio stream then it will print "1", 10 audio stream would print out an "A", 11 will be "B", etc. In the example above we see K, L and M, which is 20, 21 and 22 streams, which is very good. Generally speaking, you will want 12 "C" or better.  If a particular part of your SD card is bad, you may see numbers instead of letters, and you may also observe freezing as the letters are printed out. Note that the algorithms on the SD card may step in and auto-fix these things, so you may get different resulst if you run it again.

Finally, at the end you'll see two histograms, one for opening files and one for reading blocks. These histograms have twenty columns per millisecond and the columns of dots generally show how many reads/opens fell into that bucket. So, if we start with the "time to open files" histogram above, we can see that:

* Most of the time, opening a file takes 2.1-2.5ms. However, some of the time, opening a file takes 3.35-3.75ms.
* Some files opened as fast as 1.35ms, not sure why.
* At the top it shows the average time: 2561.39 us (2.56139 ms)

Please note that a good average isn't always enough. It could be that there is one file that takes 12ms to open, but the average is still low. This is why we have a histogram so taht we can see what the spread of results actually is.

Moving on to the block read histogram, we can see that:
* The average speed is: 1924.88 kb/s, which is 21.82 simultaneous audio streams. This is a good result. 12 or more is required.
* The vast majority of block reads take 0.2-0.25ms - which is good.
* The worst block read took 0.5ms - which is pretty normal.

Please note that "sdtest" only tests the files of the current font by default, however you can do "sdtest all" to to have sdtest read all files on the sdcard. This takes longer of course, but will tell you if any of the fonts on the SD card has problems.

# Solutions

Obviously "get a new SD card" will solve all of these problems - assuming you get a good SD card, which isn't always easy. However, formatting the SD card and re-loading all the files often works quite well. This can also solve corruption problems, which usually are caused by user errors, OS bugs or bad cables rather than bad SD cards. For slow cards, I would recommend getting a new card even if formatting seems to help. Most likely, the slowness will come back.

For formatting the SD card I recommend using [the SD card association formatter](https://www.sdcard.org/downloads/formatter/). Other ways to format may be fine, but some use partitions or file systems that ProffieOS doesn't support. If you use something else to format and it doesn't work, please try the SD card association one.

# A note about corruption
Almost all SD card corruption is caused by the same thing: Interrupted SD card writes.
There are basicaly two this can happen:

1. ProffieOS is writing to the card when you turn it off.
2. Your computer is writing to the SD card when it is disconnected from the computer.

From ProffieOS 7.x, a new save file format was introduced, which makes it so that any corruption caused by interrupted writes are harmless, so long as they don't cause the SD card to freeze and never return. Basically (1) should not be a concern anymore.

For (2), a little caution goes a long way, make sure you do this:
* if you have "mass storage" on, always select "eject safely" before disconnecting the board from your computer.
* Also use "eject safely" before hitting "upload" in Arduino. An upload will reboot the board, which also disconnects it.
* After "eject safely" make sure to wait until the little popup says you can remove the board. This can take several minutes if you copied fonts to the SD card. Even hours if you copied a lot of fonts.
* In ProffieOS 8.x there is an defined called MOUNT_SD_SETTING which will prevent your computer from accessing your SD card when you don't want it to. I highly recommend using this define to avoid SD card corruption.
  



