---
title: How to add a blade
---

So you got a second saber, and it has more LEDs than your first one? Maybe it has a crystal chamber, or an illuminated pogo pin PCB. So now you want to take your existing configuration file and add another blade for the extra LEDs. You've come to the right place.

We'll need to do four things:
1. remove KEEP_SAVEFILES_WHEN_PROGRAMMING if present
2. increase NUM_BLADES by one
3. add another blade in each entry in the blades[] array
4. add another style to each preset in your config file

## Step 1, remove KEEP_SAVEFILES_WHEN_PROGRAMMING if present
If you have [KEEP_SAVEFILES_WHEN_PROGRAMMING](/config/the-config_top-section.html#keep-savefiles-when-programming) in your config file, you need to remove it, because it's not going to work when you add another blade.

## Step 2, increase NUM_BLADES by one.
Simple, just change:
```
#define NUM_BLADES 1
```
to:
```
#define NUM_BLADES 2
```
## Step 3, add another blade in each entry in the blades[] array
This is a little trickier. Your blades array may look like this:
```
BladeConfig blades[] = {
 { 0, WS281XBladePtr<132, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(), CONFIGARRAY(presets) },
};
```
Now, let's say we have a crystal chamber with two LEDs, once we add the second blade, it might look like this:
```
BladeConfig blades[] = {
 { 0,
   WS281XBladePtr<144, bladePin, Color8::GRB, PowerPINS<bladePowerPin2, bladePowerPin3> >(),
   WS281XBladePtr<2, blade4Pin, Color8::GRB, PowerPINS<bladePowerPin6> >(),
   CONFIGARRAY(presets) },
};
```
This assumes that the data for your crystal chamber comes from LED4, and the (-) pad is hooked up to LED6. If that's not the case, you'll need to modify this example accordingly. You can also use the configuration generator to generate blades arrays which might look more like your specific setup to make it easier.

## Step 4, add another style to each preset
The style will determine the color for your new LEDs, and obviously, you can use anything you want, but for simplicity, I'm going to show three easy options to get you started:

### Option 1, copy the existing style.
So if your preset looks like this:
```
  { "TeensySF", "tracks/venus.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    "cyan"},
```
Then you just copy the style, and the comma after it, like so:

```
  { "TeensySF", "tracks/venus.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    "cyan"},
```

Now the new LEDs will behave exactly like the main blade. That might not be what you actually want, but it's always a good idea to keep it simple first and make one more change at a time.

## Option 2, get a style from somewhere
You can use the style generator, take a style posted somewhere, or one that came with a sound font. You just insert the new style after the old one, exactly like we did above, the result might look like:


```
  { "TeensySF", "tracks/venus.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    StylePtr<SimpleClash<Lockup<Blast<Cylon<Rgb<0,0,64>,15,10, DeepSkyBlue,15,100,2000,Cylon<Rgb<64,0,0>,15,6, Red,15,57,2000,Cylon<Rgb<0,40,0>,15,7, Green,15,37,2000>>>,White>,AudioFlicker<Blue,White>>,White>>(),
    "cyan"},
```

This is just an example of course, the style you use might be much shorter. (Or, in some cases, much longer.)

## Option 3, make the new LEDs black
This can be nice for some presets that don't need the extra bling. In this case we simply set the new style to black, like so:
```
  { "TeensySF", "tracks/venus.wav",
    StyleNormalPtr<CYAN, WHITE, 300, 800>(),
    StylePtr<Black>(),
    "cyan"},
```

Now, please note that you may have a charging style that looks something like this:

```
  { "TeensySF", "tracks/mars.wav",
    &style_charging,
    "Battery\nLevel"}
```
Note that "&style_charging" *is* a style, even if it looks different from most other styles. All the options above apply the same. Here is what it would look like if make the crystal chamber off/black while charging.
```
  { "TeensySF", "tracks/mars.wav",
    &style_charging,
    StylePtr<Black>(),
    "Battery\nLevel"}
```

Ok, so there you go. Save the config file and upload your new configuration.
