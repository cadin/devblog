---
layout: post
title: "Adding Text to Panels"
tags:
  - code
  - panels
carousel:
featured:
---

I want the Panels framework to be able to support live text layers. You could of course bake the text into the graphical layers in your comic, but it would better to have them as live text in cases where you want to support localization, dynamically generated text, or text that animates on and off the screen letter by letter.

Here's an example of an animated computer screen panel I put together for my game:

![Computer screen animation with text typing on and blinking](/images/posts/2021-08/textScreen.gif#playdate)

## Basic Text

Adding a text layer to a panel is as easy as specifying the string and its location within the panel:

```lua
layers = {
  {
    text = "SYSTEM.LOG", x = 16, y = 8,
    background = Panels.Color.BLACK, font = "fonts/font-Cuberick-Bold"
  },
}
```

Since my text appears over an image, I added a solid background behind the text by specifying the background color. I can also specify the text color, but the system is smart enough to use the opposite of the background color when there is one.

## Custom Fonts

I also want to use a custom font, so I could specify that here on the layer. In my case, I'll be using the same font for multiple layers in this panel, so I can actually set the default font to use for the entire panel, instead of having to list it for each individual layer:

```lua
{ -- panel container
  font = "fonts/font-Cuberick-Bold",
  layers = {
    { text = "SYSTEM.LOG", x = 16, y = 8, background = Panels.Color.BLACK },
    { text = "TOUCHDOWN", x = 16, y = 130, background = Panels.Color.BLACK }
  }
}
```

## Effects

I want some of this text to type on as the panel comes into view, so I can add an animation effect like this:

```lua
{
  text = "TOUCHDOWN", x = 16, y = 130,
  background = Panels.Color.BLACK
  effect = {
    type = Panels.Effect.TYPE_ON,
    duration = 300, delay = 500
  }
}
```

The `TYPE_ON` effect types the text on incrementally over the specified `duration`. You can `delay` the start of the animation to wait for the transition animation or other text animations to finish before starting.

Text layers can also use the same `BLINK` effect that image layers use, with durations for on and off to customize the blink speed:

```lua
{
  text = "PROCEED", x = 262, y = 169,
  background = Panels.Color.BLACK
  effect = {
    type = Panels.Effect.BLINK,
    durations = {on = 750, off = 500}, delay = 2500
  }
}
```

## Putting it All Together

Here's the complete definition for this panel:

```lua
{
  borderless = true,
  frame = { margin = 24 },
  font = "fonts/font-Cuberick-Bold",

  layers = {
    { image = "shared/scanlines.png"},
    { text = "SYSTEM.LOG", x = 16, y = 8,
      background = Panels.Color.BLACK,
    },
    { text = "TOUCHDOWN", x = 16, y = 130,
      background = Panels.Color.BLACK,
      effect = {
        type = Panels.Effect.TYPE_ON,
        duration = 300, delay = 500
      }
    },
    { text = "Gomul Jungle, Callisto", x = 16, y = 150,
      background = Panels.Color.BLACK,
      effect = {
        type = Panels.Effect.TYPE_ON,
        duration = 500, delay = 1000
      }
    },
    { text = "MJD: 2590433.655520833", x = 16, y = 170,
      background = Panels.Color.BLACK,
      effect = {
        type = Panels.Effect.TYPE_ON,
        duration = 500, delay = 1700
      }
    },
    { image = "s01/AA-proceed.png", x = 262, y = 169,
      effect = {
        type = Panels.Effect.BLINK,
        durations = {on = 750, off = 500}, delay = 2500
      }
    },
  }
},
```

(Note: I'm actually using an image here for the blinking "PROCEED" because of the arrow graphic.)

---

# Font Caching

As I was putting together the part of the system that handles custom fonts, I realized a was loading a new font each time one was specified, even if the same font was used for each layer. I needed a way to check if a font has already been loaded, and if so, to reuse that font instead of loading a fresh copy.

I added a simple caching system that stores loaded fonts in a table, using the font paths as keys:

```lua
local cache = {}
function Panels.Font.get(path)
  if cache[path] == nil then
    cache[path] = playdate.graphics.font.new(path)
  end
  return cache[path]
end
```

So when I encounter a custom font I can call `Panels.Font.get("path/to/font")`. If nothing exists in the cache table with that path, a fresh font will be loaded, added to the cache and returned. Otherwise, I just return the already loaded font from the cache.

---

# Game Credits

I'm also adding a screen to the framework where users can specify a scrolling list of credits to display:

![Game credits screen](/images/posts/2021-08/creditsScreen.png#playdate)

There are some slight differences from the panel context, but it's mostly using the same basic ideas. To add credits just list the text you want to display as separate lines. Each line can have a custom font and alignment, or you can specify the same settings for the entire screen.

Since this text gets laid out in a simple list, there's no need to specify positions for each line, but you can add `spacing` before any line to separate sections of text:

```lua
credits = {
  alignment = Panels.TextAlignment.CENTER,
  font = "fonts/custom-font",

  { text = "*The Botanist*" },
  { text = "An adventure comic" },
  { text = "by Cadin Batrack" },

  { text = "*Art*", spacing = 16, },
  { text = "Cadin Batrack" },

  { text = "*Music*", spacing = 16 },
  { text = "Cadin Batrack" },

  { text = "*Story*", spacing = 16 },
  { text = "Cadin Batrack" }
}
```

(Users can also insert images into this screen to further customize the look.)
