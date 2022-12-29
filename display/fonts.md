---
title: "OLED display fonts: StarJEDI or Aurabesh"
redirect_from:
  - "/oled-display-fonts:-starjedi-or-aurebesh.html"
  - "/oled-display-fonts:-starjedi-or-aurebesh.md"
---
To have the "name" argument at the end of a blade style display the correct characters, it should be understood that
the StarJedi font maps ACSII to glyphs with all kinds of characters aside from alphabetical, as well as some that have stylized differences.  
The font shows as all capitals, but for most cases, **_you should use all lowercase letters_** to assure it will display as the characters you expect.  
For example, an R can either have the long tail as in the Star Wars logo, or it can be shorter to work with other letters.    
Lowercase 'o' is 'O', but a capital 'O' is a stylized 'N'.  

If you install the font on your computer (it's in ProffieOS/display), and choose it as the font in a text editor, you can run through the whole keyboard and see what each character generates.  

Additionally, to have the "name" argument at the end of a blade style be displayed in Aurebesh language,  
add `#define USE_AUREBESH_FONT` to the config file.

Tip:  
If you want to split the message up across 2 lines use a newline \n, so like:  
"darth\nvader"  
or if you want to get fancy, use a couple of spaces to center it on the screen  
"   darth\n   vader"
