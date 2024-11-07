---
title: OLED images and animations
redirect_from:
  - "/oled-images-and-animations.html"
---
ProffieOS can load images and animations from the SD card and display them on an OLED display screen.  
Currently, the following events can play them:  
* boot (when power is applied to the board),  
* font (when a new preset is selected)  
* on (when blade is running)  
* idle (when blade is not running)  
* clsh
* blst
* force
* lock

From ProffieOS 7.x, these additional events are available:
* preon
* out
* in
* pstoff

In the future, there will probably be more things that will trigger loading OLED images or animations from the SD card, as well as additional size displays, including color, etc..
For this page's explanations, a typical monochrome 128x32 pixel OLED display is used as the example target.
   
ProffieOS uses the same code to locate image files as it uses for sound files.  
This means that multiple numbered files can be used, and one of them will be selected randomly to show each time.  
During boot, ProffieOS will look in the first font directory of your font search path for "boot.bmp", "bootNNN.bmp", "boot.pbm" or "bootNNN.pbm" (where NNN is a number).  
During preset changes, ProffieOS will look in the font directory for "font.bmp", "fontNNN.bmp" "font.pbm" or "fontNNN.pbm", and so on for the other effects as well.  
*Note - "font" is used as the example throughout this page. The same steps apply for on, boot, and the rest of the effects.  
 
For monochrome displays, two image formats are supported: bmp and pbm.  In each case, files must be formatted to fit the 128x32 screen and only use 1 bit-per-pixel (black and white only, not greyscale).  
In addition, pbms must be saved in binary format, not ASCII.  
One thing to note is that bmp files may play inverted (black->white, white->black) so the resulting files can be inversed later if they don't appear as intended on the OLED display.  
pbm files seem to avoid this inversion. 

Images shown on the display can be single frame stills, or they can be animated.  
They can be created in an image editor like Paint or Photoshop, or online such as at https://www.pixilart.com.  
To get started, save each animation frame as its own image file, 128x32, and make sure the names of the exported files are sequential, like  
font001.jpg font002.jpg font003.jpg etc...  
The file type here doesn't really matter (jpg, bmp, png, etc...) as long as they are all the same. However, png gives weird results when previewing as a gif.  
The file name extension will be used in the commands below to process the image down to a 1bpp monochrome image, formatted as either bmp or pbm. 

## Install Imagemagick
We can streamline the processing with **command line tools**. (Converting exported slices/layers from Photoshop for example)  
For a step-by-step video, you can see : https://www.youtube.com/watch?v=-OCy1dyW7EQ  
By using Imagemagick, we can process images appropriately, and convert to 1bpp (1 bit-per-pixel) monochrome image file in one step.  
The source file type doesn't matter, as long as they are all the same and part of a numbered sequence of file names.  
For example, Photoshop slices out to .jpg files, so we process all the numbered files of the specified file type.  
Imagemagick used to use "convert" for the command, but now uses "magick" instead (although as of this writing, "convert" still works, just with a note of the changeover).  
 
Windows: Download the installer here : https://imagemagick.org/script/download.php  
Be sure to turn the checkmark ON for "Install legacy utilities" during the installation.  
Once installed, type `cmd` in the search box near the Start menu to open a command prompt,  
then navigate to the directory containing your numbered image files by using the `cd` command.  

MacOS: To install Imagemagick on MacOS, open Utilities/Terminal, copy and paste this:  
`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`  
When it’s done, this: `brew install imagemagick`  
When that’s done, this: `brew install ghostscript`   
<br/>
<br/>
Animations for the OLED display can play either looped, or non-looped.  

## Looped Animations  
To make a looped animation, use bmp files, stacking frames vertically. For instance, a bmp image that is 128x64 is a 2-frame looped animation. 128x96 is a 3-frame looped animation, etc.  
Use the "magick" command with "-append" (which stacks the frames vertically) and "-monochrome" flags, which looks like this:  
( * is a wildcard so all files enging in ".jpg" will be processed)  
`convert -append -monochrome *.jpg font.bmp`  
The resulting file named "font.bmp" is now ready to play on the OLED.  
   
## Non-looped Animations  
To make non-looped animations, we need to concatenate the files together into a pbm file without the vertical stacking.  
We can use the same Imagemagick "magick" command as above, just without the "-append" option.  
`convert -monochrome *.jpg font.pbm`

## Convert from bmp to pbm, or vice-versa
The idea here is simply to break out a file (back) to its individual frames and then make the desired file type.  
Example: Make a currently looping 128x3648 boot.bmp into a non-looping boot.pbm file.

1. Stick a copy of the file in a new, empty working directory, and calculate the number of frames by dividing the total vertical pixels by 32. (3648/32=114)  
2. `cd` to that directory, then use that number in this command  
`convert boot.bmp -crop 1x114@ frame-%04d.jpg`  
This is going to give you 114 files (one per frame) named “frame” with 4 digits and .jpg extensions.  
3. Take all the files that start with “frame” and make a .pbm file.  
`convert -monochrome frame* boot.pbm`  

On Linux , this can be optionally done with the "cat" command, however we need to either process files that are monochrome already, or convert the result of this:  
`cat frame????.jpg >font.pbm`


## Converting video to frames
While Imagemagick can also use "convert" to break out a video file to individual frames for processing, ffmpeg does a better job.  
To install ffmpeg for Windows, see here https://www.geeksforgeeks.org/how-to-install-ffmpeg-on-windows/  
To install ffmpeg on MacOS, see here https://phoenixnap.com/kb/ffmpeg-mac  
Videos with .mp4 and .mov extensions have been tested, others likely work as well.  

This command will make numbered files for EACH frame of the video.  
`ffmpeg -i SourceFileName.mp4 frame%04d.jpg`  
Now, that command as-is may generate too many frames depending on your video length, so you can optionally choose an interval by using the `-r` flag like this:  
`ffmpeg -i SourceFileName.mp4 -r 1 frame%04d.jpg`  
Using the option `-r 1` will set the output frame rate to 1 every second. Assuming the input video has a frame rate of 30 per second, `-r 1` will output about every 30th frame.  
Calculate the interval you need according to the frame rate of the input. For example, to get approximately every 10th frame, use `-r 3.0`.
The output file name uses `%04d` which creates a numbered sequence with four digits, so frame0001.jpg, frame0002.jpg, and so on.

Once all of the frame files are available, making a .bmp or .pbm from them is the same as explained above.


## Seeing a preview of the results 
An easy way to preview the bmp image/animation is to just drag it into a Chrome browser window.
The bmp file should look tall, stacked for as many frames as you processed (some lengthy animations are very tall skinny images).  
  
The non-looping pbm file won't view in the same way, so while it's pretty easy to just copy it to the SD card and actually view it on the OLED itself, there is another way to preview it, again using Imagemagick.  
Make a gif file from the frames, and then it CAN be dragged onto the browser window to watch the playback.  
*Note - while gifs of pbm files will loop in the browser, the pbm will play once on the OLED using ProffieOS.
The delay speed used here is pretty close to on-display speed when set to ~3 as seen below.  
`convert -delay 3 *.jpg preview.gif`  
If we wanted to "boomerang" the animation by adding a reversed order of frames to the end,   
we make the gif as above, then use this command:  
`convert preview.gif -coalesce -duplicate 1,-2-1 -quiet -layers OptimizePlus -loop 0 boomerang.gif`  
The gif could even be converted back to bmp or pbm.  
`convert boomerang.gif font.pbm`


## Inverted color results
If the final bmp image/animation is an inverted black and white color scheme from what you intended,  
simply redo the conversion as above, but this time add the `-negate` flag, like:  
`convert -monochrome -negate *.jpg font.bmp`

## Orientation
Lastly, if the image is displayed upside down on the installed screen, we can easily rotate it 180 degrees by adding  
a define to the CONFIG_TOP section of the uploaded config file:  
```cpp
#define OLED_FLIP_180
```
There's also an option to flip it mirror image:  
```cpp
#define OLED_MIRRORED
```
