---
title: Blade Styles
---
Blade styles specifies the look and behavior of the "blade". I put "blade" in double quotes, because every accent led, motor or other thing you can control is generally also a "blade".

Blade styles are made by combining style templates. Style templates are sort of mix between layers in gimp and "functions" from high school math. When you use one, it looks like this:

    StyleTemplateName<FirstArgument, SecondArgument, ThirdArgument>

As you can see, it looks just like using a function, but with < > instead of ( ). The interesting part is that these can be nested, so the arguments can also be used as functions, like this:

    StyleTemplateName<OtherTemplate<Arg1, Arg2>, AnotherTemplate<Arg>, ThirdArgument>

Important - always check that you have not forgotten to close every opening < with a > and that there's a comma used in between each argument.

A style template that takes no arguments, can be written in two ways:

    Rainbow<>
    Rainbow 

Now, there is one more thing we need to know, which is that not all arguments are the same. For instance, if you have a template that expects that the first argument is a number, you can't just put a color there and have it work. For our purposes, these are the categories we care about:

* COLOR: Most common type of argument, these sort of work like layers in gimp
* INTEGER: A simple number
* FUNCTION: A style template that returns a number.
* TRANSITION: Defines how to go from one color to another

So if a template expects an argument of a particular type, you must give it an argument of that type, and not some other type, or it won't work. Here are some basic examples:

    Rgb<255,0,0>   // COLOR (red in this case), takes three INTEGERs as arguments
    10             // INTEGER
    Int<10>        // FUNCTION (this function always returns 10)
    TrFade<100>    // TRANSITION (fade from one color to next in 100ms)
    Rainbow        // COLOR (always changing)

Finally, in order to actually _use_ a blade style, we have to wrap it in something that will create the style and return a pointer to it. This might not make any sense unless you know C++, but all you need to really know is that once you have made a blade style, you have to wrap it in SylePtr<YOUR STYLE HERE>() to actually use it.
There are other ways to do this, like StyleNormalPtr(), but ultimately, they are just shorthands for a longer style that uses StylePtr<>.

Now, let's dissect a very simple blade style to understand what it does:

    StylePtr<InOutHelper<SimpleClash<Lockup<Blast<Blue,White>,AudioFlicker<Blue,White>>,White>, 300, 800>>()

To better see how the arguments work, we can re-format it like this:

    StylePtr<
        InOutHelper<
            SimpleClash<
                Lockup<
                    Blast<
                        Blue,              // base blade color
                        White              // blast color
                    >,                     // end of blast
                    AudioFlicker<Blue,White>   // lockup color
                >,          // end of lockup
                White>,         // second argument to SimpleClash  
            300,                // second argument to InOutHelper
            800                // third argument to InOutHelper
        >      // end of InOutHelper
    >()        // end of StylePtr

This is a still a valid blade style, which can be placed in your config file as is. The config file will not care if there are some extra spaces or newlines or comments inside your style. Let's walk through it from inside to out.

* Blast<Blue, White>: Blue is the base color of this blade. Blast<> adds a white effect to it when the blast effect is triggered.
* Lockup<..., AudioFlicker<Blue, White>>: This adds the lockup (and drag) effects to the blade. The color used for the lockup uses AudioFlicker<Blue, White> to produce an unstable flickering effect between white and blue.
* SimpleClash<..., White>: This adds a white clash effect
* InOutHelper<...., 300, 800>: This adds extension (300ms) and retraction (800ms)


Here is where you can find all the possible style templates:
* COLOR https://github.com/profezzorn/ProffieOS/tree/master/styles
* FUNCTIONS https://github.com/profezzorn/ProffieOS/tree/master/functions
* TRANSITIONS https://github.com/profezzorn/ProffieOS/tree/master/transitions

Note - There are default values for style templates. These can be found in the files located in the styles folder. Arguments with default values can be left out, which makes it easier and shorter to write out the style, however, it can be difficult to know that those arguments are available if you are trying to change something in an existing blade style. The style editor will show all arguments for a style, so you can use it find arguments that you otherwise cannot see.
 
For example, SimpleClash has a default duration of 40. In the example above, that argument is not shown, but it is nevertheless there. If you use the style editor you will see it, or if you look up the [documentation for SimpleClash](https://github.com/profezzorn/ProffieOS/blob/094b3f482d1981d47235bb40773c6424214f2b69/styles/clash.h#L6) you can see that the full template is:

    SimpleClash<BASE, CLASH_COLOR, CLASH_MILLIS>

So for a Red blade that clashes White for 80 milliseconds, you would need to add the 80 (non default) value in the appropriate argument's position in the template, like so:

    SimpleClash<Red, White, 80>
 
For a working list of many templates, some with default values included, along with Functions and Transition syntax, see here:
[TEMPLATES SYNTAX SUMMARY](http://therebelarmory.com/thread/11489/templates-syntax-summary)

To experiment with them and figure out how to use them, I recommend using the [style editor](https://fredrik.hubbe.net/lightsaber/style_editor.html).

Also, you can find lots of pre-made blade styles in the [Style sharing thread on TheRebelArmory.com](http://therebelarmory.com/thread/9273/teensysaber-blade-style-sharing-thread).
