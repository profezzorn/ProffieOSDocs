---
title: Save File Format
---

Up until ProffieOS 6.x all save files in ProffieOS were basically simple INI files. Just a bunch of lines like:

```ini
variable=value
anotherVariable=value
end
```

While super simple, it did cause some problems, because saving these files deleting or overwriting files, and every time you write to the SD card, there is there is a chance that the write could be interrupted in the middle, making one or more blocks turn into gobblygook. Now, if the data inside the file turns into gobblygook, that isn't really a problem. We have a .bak file for that. Also, the "end" written at the end of the file lets us check if the file was written all the way to the end or not.

However, if the gobblygook occurs while creating or deleting a file, then the directory itself becomes corrupt, and that can mean files and directories just can't be found anymore. In some cases, this makes the SD card completely unreadable.

In ProffieOS 7.x, this problem has been mostly solved. The solution is to create the files once, make them big enough to contain all the data we could ever want to write to them, and then re-write them. By never creating new files, and never resizing the files, only the contents of the files can become corrupt, not the directories. At least as longas the SD card itself doesn't go crazy.

To make this work, we'll need two files for each save file, and we'll take turns writing to them. That way, we never overwrite the last savefile, we only write over the last-last savefile.

Of course, we'll need some way to tell which file was is actually the newest one. We'll solve this by writing a number into the file which increases by one every time we save. That way, the file with the highest number will be the last one.

We'll also need some way to know if the file gets corrupted for some reason. If that happens, we'll read the previous file. If we loose power in the middle of writing to a file, when we read the file, we should be able to discover that it was corrupted. For this, we'll use a checksum, if you don't know what a checksum is, google it.

Finally, we'll need a way to know how long the data in the file is. Since the file is going to be much longer than we need, we can't rely on the length of the file itself to tell us how much data is in the file anymore.

## The actual format
```cpp

struct Header {
  uint32_t magic_number;  // 0xFF1E5AFE
  uint32_t checksum;
  uint32_t iteration;
  uint32_t length;        // Length of the data, starting from the second block.
};

struct FirstBlock {
  Header header1;
  Header header2;
  char install_time[480];
};
```

The header is repeated twice, followed by the install time, and then enough zeroes to fill up the first block (512 bytes). Unless KEEP_SAVEFILES_WHEN_PROGRAMMING is defined, save files with a different install_time than the currentntly running program will be ignored. Files where header1 is different from header2 will also be ignored. Or where the checksum doesn't match the checksum of the data in the file. If neither of the two files pass all of these tests, ProffieOS will try to read the files as plain ini-files instead, which makes all of this backwards compatible. However, when it writes new files, those files will be in the new format.

If you wish to edit a config file by hand, please be aware that you can't just skip the first 512 bytes and make a change in the file, because the checksum won't match anymore. However, you can *delete* the first 512 bytes from the file, then make the edits and save the file. The result will be a regular ini file, which ProffieOS can read in compatibility mode. Note that you'll need to delete the *other* file though, or ProffieOS will prefer that one.

Basically, ProffieOS will do the following:
1. check if the .ini file is in the new format, and is valid
2. check if the .tmp file is in the new format, and is valid
3. If both are true, it will read the one with the highest iteration number
4. If only one is true, it will read that file
5. If neither is true, it will try to read the .ini file as a plain ini file.
6. If that fails, it will try to read the .tmp as a plain ini file.


