First up: The arduino program has a small region at the bottom where it shows error messages in red text. Unfortunately it usually scrolls past the first error message and only shows you the last part, which is not very helpful. Make the error region larger and scroll up to find the first error message. Read on to learn what usually causes the errors, and how to find and fix them.

If you see this error:
`#error Tools->DOSFS should be set to SDCARD (SPI)`
Go to the Tools menu, find DOSFS and set it to "SDCARD (SPI)" and try again.

If you see a lot of red text compile errors, don't be discouraged thinking there's a lot of things wrong. Usually, just the first error shown is the actual problem, and all of the following messages are just a result of a cascade effect. 
The most common errors are in the presets section of the config file (my_saber.h for example) where edits to presets have occured. It's quite easy to make a typo, specifically leaving out a code punctuation (comma, < or >, a parenthesis,  a brace etc...). Many times styles can be copied from the [Style Editor] or elsewhere and pasted in the config file without having a comma added, or the whole line to be replaced was selected, including the comma, and then pasted over.
Each blade style must be followed by a **comma**, unless the preset description at the end is being omitted, leaving the blade style as the last element, where it then just gets followed by a closing brace comma **},** 
Each style's arguments must open with < and close with >. Again, missing just one of these punctuations will cause the compile to fail. This is easy to miss once looking at long lines in a style or multiple nested templates, such as:
> AudioFlicker<Blue,Rgb<128,0,128>>
 
is sometimes left as just
> AudioFlicker<Blue,Rgb<128,0,128>

It looks complete at a quick glance. However, the Rgb has its closing > but AudioFlicker also needs one, and visually it's easy to miss until you get very used to seeing it.

The second most common issue is a mismatch of number of blades defined in the CONFIG_TOP section and the number of blade styles contained in the preset(s). Each LED wired to an LED pin on the board counts as a "blade", even if it's a single accent LED. If you have 1 main blade and 2 accent LEDs, 3 "blades" must be defined with #define NUM_BLADES 3, and all of the presets must contain 3 complete blade styles. 

The error message in Arduino gives the best clue as to where the problem exists in the form of a line number of the config file causing the problem. For this reason, it is highly suggested to use a text editor that uses line numbering for troubleshooting the problem with the config file.
In the following example error message, Just before the first occurance of the word "error" is the line number, and there's a caret symbol pointing up to the issue. 
```
In file included from /HardDrive/Lightsabers/ProffieOS/ProffieOS.ino:631:0:
/var//T/arduino_build_915026/sketch/config/mysaber_config.h:47:5: error: expected '}' before 'StyleNormalPtr'
	StyleNormalPtr<WHITE, RED, 300, 800, RED>(), "white"},
	^ 
```
This tells you that when the compiler got to line 47, it was expecting a closing bracket. So we can go look at why. Here's the section with line 47 from the config:
```
{ "TeensySF", "tracks/mercury.wav",
  StyleNormalPtr<WHITE, RED, 300, 800, RED>()
  StyleNormalPtr<WHITE, RED, 300, 800, RED>(), "white"},
```
This config file uses 2 blade styles per preset, and line 47 looks fine, _and it is_. But the problem is that there is no comma after the style **ABOVE** it, so when the compiler got to the end of the first style and found no comma, it assumed it was the end of the preset, and expected a closing brace **}**
That is how you find errors using error messages from Arduino. <br>
For more info on deciphering Arduino error codes, read here:  <br>
[Error Messages in Arduino and how to decipher them.](https://github.com/profezzorn/ProffieOS/wiki/Error-Messages-in-Arduino-and-how-to-decipher-them.)

If it still doesn't compile, try Googling your error message combined with a search term "Proffie". If it shows things that are not helpful, try adding site:therebelarmory.com to your query. Chances are that someone else has had the same problem and
already asked about it on the forums.

If you still could use some help, go here: http://therebelarmory.com/thread/10207/proffieboard-newbie-thread and post your config file and complete error message, and someone will help you figure out what the problem is.

If you've made edits and it DOES compile, but you don't see your changes after uploading, see the [Troubleshooting Files and Folder Structure](troubleshooting-files-and-folder-structure.md) page.
