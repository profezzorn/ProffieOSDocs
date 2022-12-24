---
title: OLED images and animations
---
ProffieOS can load images and animations from the SD card and display them on an OLED display screen.  
Currently, the following events can play them:  
boot (when power is applied to the board),  
font (when a new preset is selected),  
on (when blade is running),  
clsh, blst, force, and lock.  
In the future, there will probably be more things that will trigger loading OLED images or animations from the SD card.  
   
ProffieOS uses the same code to locate image files as it uses for sound files.  
This means that multiple numbered files can be used, and one of them will be selected randomly to show each time.  
During boot, ProffieOS will look in the first font directory of your font search path for "boot.bmp", "bootNNN.bmp", "boot.pbm" or "bootNNN.pbm" (where NNN is a number).  
During preset changes, ProffieOS will look in the font directory for "font.bmp", "fontNNN.bmp" "font.pbm" or "fontNNN.pbm", and so on for the other effects as well.
* Note - "font" is used as the example throughout this page. The same steps apply for on, boot, and the rest of the effects. 
 
Currently, two image formats are supported: bmp and pbm.  In each case, files must be formatted to fit a 128x32 screen, or 32x128 and only use one bit per pixel.  
(a.k.a. 1bpp, monochrome, two colors). In addition, pbms must be saved in binary format, not ASCII.  
One thing to note is that bmp files will play inverted (black->white, white->black) so the resulting files should have the colors "backwards" of how we want them to appear on the OLED display.  
* This can be easily fixed later if you forget the "backwards" part, and pbm files seem to avoid this inversion. 

Images can be single frame stills, or they can be animated.  
They can be created in an image editor like Paint or Photoshop, or online such as at https://www.pixilart.com.  
To get started, save each animation frame as its own image file, 128x32, and make sure the names of the exported files are sequential,   like  
font001.jpg font002.jpg font003.jpg etc...  
The file type here doesn't really matter (jpg, bmp, png, etc...) as long as they are all the same.  
The file name extension will be used in the commands below to process the image down to a 1bpp monochrome image, formatted as either bmp or pbm. 

## Install Imagemagick
We can streamline the process of combining multiple images with command line tools. (exported slices/layers from Photoshop for example)  
For a step-by-step video, you can see : https://www.youtube.com/watch?v=-OCy1dyW7EQ   
 
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
To make a looped animation, we simply make the image taller than it is wide, stacking frames vertically. For instance, if we make our image 128x64, that will be a 2-frame looped animation. 128x96 is a 3-frame looped animation, etc.  
Then, by using the "convert" command with "-append" and "-monochrome" flags, we can stack the images appropriately, and convert to 1bpp monochrome in one step. The source file type doesn't matter. For example, Photoshop slices out to .jpg files, so we process all the numbered files of the specified file type.  
( * is a wildcard so all will be processed)  
`convert -append -monochrome *.jpg font.bmp`  
This file is now ready to play on the OLED.  

   
## Non-looped Animations  
To make non-looped animations, we need to concatenate the files together into a pbm file without the vertical stacking.  
We can use the same Imagemagick "convert" command as above, just without the "-append" option.  
`convert -monochrome *.jpg font.pbm`

On windows, this can also be done with the "copy" command, like so:  
`copy /b *.jpg font.pbm `  

On Linux , this can be done with the "cat" command, however we need to either process files that are monochrome already, or convert the result of this:  
`cat font???.jpg >font.pbm`


## Converting mp4 to frames
We can also use "convert" to easily break out an mp4 video file to individual frames for processing.  
Again, file type can be different, (jpg, bmp, etc..) Just use the correct one in the subsequent commands.
This time, we'll make numbered bmp file frames for the font image.  
`convert file.mp4 font.bmp`  
The result here will be one bmp file for each frame of the movie clip, numbered sequentially.  
Then, we process them the same way as above with one of the the previous commands, this time maybe using `font*.bmp` in case there are other named bmps we don't wish to include by using full wildcard as in `*.bmp`.  
 
We can directly convert an mp4 file into a non-looping pbm animation.  
For this, you should use a file pre-cropped to 128x32:  
`convert file.mp4 font.pbm`

## Seeing a preview of the results 
An easy way to preview the bmp image/animation is to just drag it into a Chrome browser window.
The bmp file should look tall, stacked for as many frames as you processed (some lengthy animations are very tall skinny images).  
  
The non-looping pbm file won't view in the same way, so while it's pretty easy to just copy it to the SD card and actually view it on the OLED itself, there is another way to preview it, again using Imagemagick.  
Make a gif file from the frames, and then it CAN be dragged onto the browser window to watch the playback.  
* Note - while gifs of pbm files will loop in the browser, the pbm will play once on the OLED using ProffieOS.
The command to make the gif is very similar.  
* Note - the delay speed here is pretty close to on-display speed when set to ~3 as seen below.  
`convert -delay 3 *.jpg preview.gif`  
If we wanted to "boomerang" the animation by adding a reversed order of frames to the end,   
we make the gif as above, then use this command:  
`convert preview.gif -coalesce -duplicate 1,-2-1 -quiet -layers OptimizePlus -loop 0 boomerang.gif`  
then just convert back to bmp or pbm.  
 `convert boomerang.gif font.pbm`


## Inverted color results
If the final bmp image/animation is inverted colors on the OLED itself, a simple fix could be:  
- opening the file in MSpaint, (or the online java script based version at http://jspaint.app)  
- choose menu Image>Invert Colors,     
- File>Save and save as Monochrome Bitmap. The browser downloads to the set downloads location.  

## Orientation
Lastly, if the image is displayed upside down on the installed screen, we can easily rotate it 180 degrees by adding  
a define to the CONFIG_TOP section of the uploaded config file:  
`#define OLED_FLIP_180`  
There's also an option to flip it mirror image:  
`#define OLED_MIRRORED`
