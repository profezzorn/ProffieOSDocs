---
title: "OLED additional features: Bullet Counts"
---
As of ProffiesOS 6.x, it's possible to show bullet counts on an OLED display.
Here's what you would need:

This includes the display code, but doesn't activate it.
May become the default in the future.
```
#define INCLUDE_SSD1306
```

Here's how we activate the display:
```
#ifdef CONFIG_BOTTOM

DisplayHelper<128, uint32_t,
  BaseLayerOp<StandardDisplayController>,
  ClearRectangleOp<10, 80, 8, 24>,
  WriteBulletCountOp<10, 20, 5>
> display_controller;

SSD1306Template<128, uint32_t> display(&display_controller);
#endif
```

The `DisplayHelper` class takes a list of display operations, which works a lot like the `Layers<>` style. Currently, these operations are available:

Two different base layers:
1. `BaseLayerOp<StandardDisplayController>`
2. `ClearScreenOp`

The first one makes it work like a standard display controller (shows, font.bmp, messages, etc., the second one just makes it black.

### `ClearRectangleOp<x1, x2, y1, y2>`
This op clears a rectangle on the screen.

### `WriteBulletCountOp<x, y, digits>`
Writes the current bullet count at the specified location.

### `IfImageOp<OP>`
This executes OP if the base layer is showing an image, but not otherwise.
The idea is that you could have a bullet count that draws over images, but not messages and battery monitors. 

We will probably need more display OPs real soon for other purposes...
In 7.x I plan to make it possible to specify a different display controller for each preset, essentially making it a "style" for the display.
