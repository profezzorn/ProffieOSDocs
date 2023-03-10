# Making changes to this site

If you find something wrong, or have an idea for how to improve
the documentation on this site. Just find the right page and
click the pencil in the top right corner. This will take you to the
right place on github.

If you don't have a github account, you'll need to create one. Once you are
signed it, github will ask you to fork the ProffieOSDocs repository, and
you'll need to do that.

After forking, you can make edits. Make sure to check the "Preview" tab to
see approximately how your changes will look once they appear on the POD site.
For more information about how to make it look the way you want, try [this site](https://www.markdownguide.org/tools/github-pages/).

Once you are happy with your changes, write a comment describing your changes
below and hit the "propose" button.

Proposing the changes will not send them directly to the POD site though.
Instead, the changes will be saved in a branch on your fork of the ProffieOSDocs repository.
If you don't know what any of that means, don't worry about it.
After pressing the "propose changes" button, github will show you a button to create a pull request. You should click this
button and create the pull request. Someone will review your changes and approve them
before they will show up on the site. This may take some time, but it also means that
you don't have to worry about making any major mistakes or breaking the site somehow.

Of course, if you already know how to use github, you can use any tools you want to fork, edit and upload pull requests.

## Best practices
Don't add newlines unless you need it. In the github editor, set it to "Soft wrap" and just write long lines to make paragraphs. This makes page resizing work better.

### Images
To make things look good in PDFs, print and retina displays, all images should be uploaded at the highest resolution available. That might come out too large when shown on the screen, and the solution is to use an "image" tag instead of using the markdown for an image.

So instead of this:

```
   ![alt text](/images/someimage.jpg)
```

you do:

```
   <image src="/images/someimage.jpg" width=400 height=200 alt="alt text" />
```

This will make the browser scale the image to 400 x 200 instead of whatever size the image was when you uploaded it, but print and retina displays will use the extra pixels to make things look good.

Uploading screenshots is good for pointing out where buttons and menues are, but not to show an error message or something like that. Information that is fundamentally text should use text, not images.

### Code

Write code blocks like this:
```
    ```cpp
    #define EXAMPLE_DEFINE
    ```
```
This will make it highlighted as C++, with a copy button, like this:

```cpp
#define EXAMPLE_DEFINE
```


## Searching for dead links (on Linux)

PS: Here is a useful linux command for finding broken links:

```
wget --spider -r -nd -nv -l 3  https://pod.hubbe.net/ 2>&1 | grep -B1 'broken link'
```

You'll need to use grep or something to find where the broken links come from though.
If you have the ProffieOSDocs github repository, you can do that with git grep, like this:

```
wget --spider -r -nd -nv -l 3  https://pod.hubbe.net/ 2>&1 | grep -B1 'broken link' | sed -n 's@https://pod.hubbe.net/\(.*\):@\1@gp'  | while read LINK ; do echo "=== $LINK ===" ; git grep $LINK ; done
```
