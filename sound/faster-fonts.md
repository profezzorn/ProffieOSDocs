---
title: Faster performance of fonts and blade animations.
---
As blade styles become more complex, combined with some pixel strips having more LEDs in serial,  
you may find less animation lag and fewer Audio  Underflows (pops, clicks, gaps) by optimizing your font folder structure.  

Sounds with multiple files should live in subfolders, such as a clsh folder containing clsh01.wav, clsh02.wav etc...  
while single files, such as hum.wav or lock.wav should live in the font root. See attached image for a visual of this.  

ProffieOS will perform best if you cater to the way that FAT32 formatting works.  

Each block can contain 16 file entries.  
If you have 128 files in one directory, ProffieOS has to read on average 4 blocks to find the the file.  
If you have 16 subdirectories with 16 files each, only 2 blocks have to be read.  
It may be possible to optimize this by adding most commonly used files (hum) first.  
Also, ProffieOS might be able to improve on this with some caching. (Future development)  
For effects that only have one sound, it should be more efficient to NOT put them into a sub-directory."  

![](/sound/images/fast1.jpg)
