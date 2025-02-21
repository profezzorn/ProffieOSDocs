---
title: PQF files
---

PQF is a file format for storing images and animations. It was inspired by the [QOI](https://qoiformat.org/) format, but re-written for 16-bit, optimized for high-speed transparency processing, and adds jumps, conditions, labels and a bunch of other things. This page will describe how to create and edit PQF files from images, but a lot of the actual capabilities of the PQF format are actually descriped on [the PQOIML page](/display/pqoiml.html). PQF files are created by using the cpqoi program, and can be disassembled by using the dpqoi program.

# Prerequisites
### A linux-like environment
* If you're already on linux: good job
* If you're on windows, you can install one using WSL, more information here: https://docs.microsoft.com/en-us/windows/wsl/install
* Mac is already mostly linux-like, but I recommend installing homebrew to make it easy to install the rest of the requirements.

### Packages you'll need
* A C++ compiler (g++ or clang++)
* ffmpeg
* mjpegtools
* netpbm

# Compiling cpqoi and dpqoi
* Download ProffieOS
* unzip it
* open up a terminal and go to the "pqoi" directory.
* run "make" to compile cpqoi and dpqoi

# Creating a PQF file from an image
Just run:
```sh
cpqoi some_image.png >some_image.pqf
```

This will create a PQF that will show the image until interrupted somehow. Note that the PQF file will have the same size as the input image, which might be too big for the display, and ProffieOS does not have the ability to scale images. To create a PQF with a specified size, you can add a scaling command, like this:

```sh
cpqoi some_inage.png "pamscale -xysize 128 80" >some_image.pqf
```

This will scale the image down until it fits in a 128x80 image. Any of the pam* commands from netpbm can be used to scale, rotate and modify the image, which can be handy for scripting.

# Creating a PQF from a movie
```sh
cpqoi somemovie.mp4 "pamscale -xysize 128 80" >animation.pqf
```
As you can see, this is exactly the same. One thing to be aware of is that this creates a looped PQF file. If that is not what you want, you will need to use a PQOIML file.

# Creating a PQF from a PQOIML file.
PQOIML files give you much more fine-grained control over the contents of the PQF file. For more information, see [the PQOIML page](/display/pqoiml.html).
```sh
cpqoi myfile.pqoiml >animation.pqf
```
Usually, with pqoiml files you'll put the scaling command in the file itself, but you can also put it on the command line, just like before:
```sh
cpqoi myfile.pqoiml "pamscale -xysize 128 80"  >animation.pqf
```

# disassembling a PQF file
You can use 'dpqoi' to inspect a PQF file, and the output can then be modified and re-assembled with cpqoi. It's recommended to run dpqoi in an empty directory, because it will write one PNG file for every frame in the PQF file.

```sh
mkdir output
cd output
../dpqoi ../animation.pqf >animation.pqoiml
```

In addition to all the PNG files, a PQOI file will be written, and if you run cpqoi on that file, it will generate exactly the same PQF file.

