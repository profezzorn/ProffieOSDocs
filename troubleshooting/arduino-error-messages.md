---
title: How to decipher Arduino error messages
---
While a bit lengthy, and hard to put into typed words, hopefully this helps you understand how to read error messages and what they are caused by.<br>
First, understand that a long list of errors does not necessarily mean there’s a ton of errors. They are just a cascade effect from the first problem.
If the compiler comes across something it doesn’t like, let’s say a brace that should be part of an open-close pair but there’s only an opening one without a closing brace, it will continue through the rest of the code trying to pair the remaining odd number of braces, finding each one mis-matched, and will spit out an error for ALL of those problems. 
If the first one gets repaired, all the others will not occur.

Fortunately, Arduino error messages indicate a line number AND character number in the message, AND give you a little caret symbol underneath one of the characters. (little upward pointing arrow, pointing at a character).
Understand that it is not necessarily pointing at the problem, but is actually pointing at the part of the code it "choked" on. 
So for example, if it was pointing at a closing brace at the end of a preset, the problem is likely a PREVIOUS character, like a missing or extra comma in the line before.
It could also be pointing at a Closing brace that it came to without having read an Opening brace first. 
In that case, back at the beginning of a section, a preset, or higher up in the config, there's a missing opening brace somewhere. In other words, it's missing it's paired brace and it's saying....close? Close what? Nothing told me to open (missing open brace)

# Incorrect number of blade styles in preset
You have to have a blade style for every "blade" defined in the Bladeconfig section at the bottom of your config file.
If you have 3 blades (a main blade, a crystal chamber LED, and another LED pixel accent for example), then there needs to be 3 blade styles in each preset.
This error, pointing to the last closing brace of the CONFIG_PRESETS section usually indicates you have a preset with too little or too many styles.
```
error: cannot convert 'const char*' to 'StyleFactory*' in initialization
 };
 ^
```  

# Transparent color as base layer
The error generated if this is the case will say:
```
error: conversion from 'RGBA_um_nod' to non-scalar type 'OverDriveColor' requested
```  
The base layer of a blade style can not be an AlphaL with transparency.
Such as:  
```
StylePtr<Layers<
  AlphaL<Red,Int<16000>>,...........
```  
The quick fix is to simply add a Black layer underneath everything else, since that won't be a visible difference, and it qualifies as a solid color as the first layer. So like:
```
StylePtr<Layers<Black,
  AlphaL<Red,Int<16000>>,...........
```  


## Example for the next few sections:
A config file named my_config.h that contains 2 blades, therefore 2 blade styles per preset. Here’s the preset:

```
17 { "JediFont", "tracks/GoodGuys.wav",
18   StylePtr<Cylon<SpringGreen,5,5,DeepSkyBlue,5,50,200>>(),
19   StylePtr<InOutHelper<DeepSkyBlue,100,100>>(),
20 "jedi" },
```

# **Missing comma after a blade style:**

A missing comma at the end of a blade style error can look like this:

```
In file included from /User/Desktop/ProffieOS/ProffieOS.ino:556:0:
sketch/config/my_config.h:19:2: error: expected '}' before 'StylePtr'
  StylePtr<InOutHelper<DeepSkyBlue,100,100>>(),
  ^
```
The pointer is indicating the first character of the second blade style. Here, you should look for what’s wrong just before this character.
In this case, even though the compiler says it was looking for a brace, it was actually a missing comma after the first blade style as seen here: 

```
17 { "JediFont", "tracks/GoodGuys.wav",
18   StylePtr<Cylon<SpringGreen,5,5,DeepSkyBlue,5,50,200>>()
19   StylePtr<InOutHelper<DeepSkyBlue,100,100>>(),
20 "jedi" },
```

This is a case where the compiler got to the end of the first style and found no comma, so it assumed it was the end of the preset, and expected a closing brace }<br>

# **Missing or an extra < or > in a blade style:**

An extra > error usually looks like this:<br>

```
In file included from /User/Desktop/ProffieOS/ProffieOS.ino:556:0:
sketch/config/my_config.h:18:57: error: expected primary-expression before ')' token
  StylePtr<Cylon<SpringGreen,5,5,DeepSkyBlue,5,50,200>   >   >(),
                                                               ^
```

The pointer is indicating a StylePtr’s close, but that’s because the compiler got to that and said…whut?? 
The problem here is that there’s an extra > before it at the end of the style (I spaced it out for visibility) and it’s messing up the order of things.
If you read the file line and character number, you’ll see it’s line 18, character 57, which is indeed the extra >.

Conversely, a MISSING > at the end of the same style, so StylePtr<Cylon<SpringGreen,5,5,DeepSkyBlue,5,50,200>(),     
makes this error:
```
In file included from /User/Desktop/ProffieOS/ProffieOS.ino:556:0:
sketch/config/my_config.h:19:45: error: call to non-constexpr function 'StyleFactory* StylePtr() [with STYLE = Layers<Rgb<0, 135, 255>, AlphaL<Rgb<0, 0, 0>, InOutHelperF<InOutFuncX<Int<100>, Int<100> >, true> > >]'
  StylePtr<InOutHelper<DeepSkyBlue,100,100>>(),
                                             ^
```

Notice how now the pointer is indicating a StylePtr’s close again, but THIS time, it’s at the NEXT style’s ending on line 19.
The missing closing > for the first style’s Cylon effect has thrown off the correct formatting, and the compiler thought the whole next line was still part of the first style.

# **Misspelling:**

The error should be pretty clear about this, just look at the thing it’s telling you “was not declared in this scope”, for example, an extra e in Green seen here:
```
In file included from /User/Desktop/ProffieOS/ProffieOS.ino:556:0:
sketch/config/my_config.h:18:17: error: 'SpringGreeen' was not declared in this scope
  StylePtr<Cylon<SpringGreeen,5,5,DeepSkyBlue,5,50,200>>(),
                 ^
```
# **Wrong Board version Selected:**
```
#error Please select Proffieboard V2 in Tools->Board
```

Self explanatory.



# **Weird Unicode character errors :**

The error message will say  something like: " error: stray '\342' ", or “stray '\200' ", or “stray '\234' "

It seems that lately this is mostly a specific problem encountered by using a newer MacOS version of Textedit, but it could happen to anyone, including even straight copy/pasting from the Proffieboard Configurator page or using Windows Notepad.

Everything will appear fine in your config file on the surface, but this error means it contains one or more stylized characters, like fancy quotation marks, italicized looking braces etc... that are not valid characters to the Arduino compiler.

The fix is to delete the offending character(s) and retype them. Sometimes it can even be a return character (invisible) so deleting back to the last character in the previous line and typing a new return sometimes is needed.
That being said, you need to make sure your text editing software is set to PLAIN TEXT. In MacOS's Textedit, this option has changed defaults lately, so go to the menubar>Format>Make Plain Text before re-typing the characters. 
This is another reason I highly suggest using SublimeText instead, as it uses proper unicode for coding, numbered lines, is color coded, and can even "spell-check" your code using linting if you want.

Here's an example:<br>

```{ "KyberTROS", "tracks/TwoThemes.wav”,```

Notice the last quotation mark is fancy/italicized.

Hard to catch, but nonetheless it is the problem.
Here's what the error would look like:<br>

```
In file included from /User/Desktop/ProffieOS/ProffieOS.ino:556:0:
sketch/config/my_config.h:17:1: error: missing terminating " character
 { "KyberTROS", "tracks/TwoThemes.wav”,
 ^
```

If you look, you can see that it didn’t like something about the file my_config.h, line 17, character 1, and in this case that’s the opening brace. Now this is not a great example because the problem lies AFTER the reported character, but this happens, and sometimes you need to look before AND after the little pointer to see what’s wrong, but it’s always close by. 
However, in this case, it DOES tell you in plain English that there’s a missing terminating " character. That’s because the ” is not the same as " . 
So there’s your problem. 
Delete the fancy/italicized weird Unicode ” with a nice plain text " , save the file, and then try Verify again.
Alternately, selecting the whole body of the file and Make Plain Text should work as well (shift+cmd+F in MacOS Textedit)

# **Base layer can't have transparency**

If you have an AlphaL as the base layer in a blade style, you'll see this error:

```
 error: conversion from 'RGBA_nod' to non-scalar type 'OverDriveColor' requested
```
The base color needs to be a non-Alpha color. Depending on the desired look, even just adding a base layer of Black will suffice.

# **Proffieboard plug-in not selected correctly**

This is a typical error message you'll see if you don't have the board selected in Arduino menu Tools>Board>Proffieboard>Proffieboard (Version)
```
FS.h No such file or directory
```

# '.text' will not fit in region 'FLASH'

This means that you've configured too many things, and ProffieOS won't fit in the available memory anymore.
See the [saving memory page](/howto/saving-memory.html) for things you can do to fix it.

