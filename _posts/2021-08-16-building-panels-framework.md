---
layout: post
tags:
  - code
  - panels
title: Building the Panels Framework
featured: yes
carousel: ""
---

![A 1-bit comic](/images/posts/2021-08/panelsComic.gif)

As I'm building my Playdate comic, I want to separate the parts that are specific to _my_ comic (the text, images, and animations) from the core functionality of displaying and navigating through any generic comic.

If I can do this successfully it will make it much easier for me to create new comics in the future. I'll be able to reuse the same functionality and just feed in new data and images to display. Ideally, the system will be flexible enough that other artists will be able to use my framework to create and publish their own comics.

I'm calling this framework **Panels**.

---

# Requirements & Definitions

## Comic

I'm starting with the assumption that a pdx built with Panels will contain one comic. This somehow feels like it fits best with the spirit of Playdate (lots of small games), and it means I don't have to worry about building in a menu to choose between multiple comics.

## Sequences

A comic can contain multiple sequences. A sequence acts like a separate chapter in most instances.

Each sequence should be able to define different settings for things like scroll direction and background color (black on white vs. white on black). I also want to have sequences that you can scroll through manually with the crank or arrows, and some that animate between panels automatically by pressing a button (or multiple buttons).

## Panels

A sequence contains multiple panels.

Panels seem to work best as full screen boxes with a small margin. But each panel can have a custom size, margin (from screen edges), and spacing (between previous panel). A panel can be drawn with or without a border.

In some cases a panel may even contain other panels.

## Layers

A panel contains one or more layers. A layer displays an image or text.

Images within a panel are split into multiple layers in order to do parallax scrolling, animation of individual elements, or other effects. Each layer can define a parallax multiplier depending on the desired depth in the image, and x and y offsets to position it within the panel.

## Effects

A layer can have an optional effect or animation applied to it. A layer can be made to shake or blink off and on, it can animate x and y position, or transition between multiple images as the panel is scrolled.

Some effects (like screen shake) can also be applied to an entire panel.

## Interactivity

Eventually, I would like to allow any single panel to define custom interaction and advance conditions. In that case, a reader won't advance past that panel until they watch an animation or complete some small mini-game in the panel.

This might be something I put off until later, depending on whether or not I need it for my first comic.

---

# Example Data File

This is all very much still work-in-progress, so the details here could change, but this currently what some data for a sequence in a Panels comic might look like:

```lua
sequence01 = {
  title = "The Climb",                   -- chapter title
  scroll = Panels.ScrollType.MANUAL,     -- manual scroll or auto-advancing
  axis = Panels.ScrollAxis.HORIZONTAL,   -- vertical or horizontal scrolling
  backgroundColor = Panels.Color.WHITE,  -- black on white or white on black
  foregroundColor = Panels.Color.BLACK,
  advanceControl = Panels.Input.A,       -- how to advance to the next sequence

  -- list of all the *panels* in this *sequence*
  panels = {
    { -- PANEL 1
      -- default frame size is full screen with 8px margin
      -- override the default to create a wider panel
      frame = {margin = 8, width = 1184},
      -- change the magnitude of the parallax movement
      parallaxDistance = 800,

      -- list all the *layers* in this *panel*
      layers = {
        { image = "s01/A-1-sky.png", parallax = 1, x = 70 },
        { image = "s01/A-2-mountains.png", parallax = 0.9 },
        { image = "s01/A-4-cliff.png", parallax = 0.5, x = -50 },
        -- etc..
      }
    },
    { -- PANEL 2
      -- this panel uses default settings for frame size, parallax, etc
      -- so no need to define them here
      layers = {
        { image = "shared/starfield.png", parallax = 1 },
        { image = "s01/B-2-cliffs.png", parallax = 0.9 },
      }
    },
    { -- PANEL 3
      borderless = true -- don't draw a border around this panel
      layers = {
        { image = "s01/C-1-BG.png", parallax = 1 },

        -- this layer has 2 images
        -- they are swapped when the panel reaches the halfway scroll point
        -- listing 3 images will swap them at 33%, and 66% scroll, etc
        { images = { "s01/C-6-fronds-A.png", "s01/C-6-fronds-B.png" },
          parallax = 0.4 },

      }
    },
    { -- PANEL 4
      layers = {
        { image = "shared/starfield.png", parallax = 1 },
        { image = "s01/D-5-marker.png", parallax = 0.5,
          -- an effect that makes this layer blink on and off
          effect = { type = Panels.Effect.BLINK, durations = { on = 500, off = 300 } }
        },
        { image = "s01/D-6-thing.png", parallax = 0.6,
            -- this layer animates from -100 y to 100 y based on scroll progress
            y = -100, animate = { y = 100 }
        },
      }
    },
    { -- PANEL 5
      -- a shake effect applied to ALL layers in the panel
      effect = { type = Panels.Effect.SHAKE_UNISON, strength = 2 },
      layers = {
        { image = "ch01/01-A-starfield.png", parallax = 0.8, y = -24 },
        { image = "ch01/01-B-shipBG.png", parallax = 0.3, },
      }
    }
  }
}
```

# Example Lua File

Since all the logic, update loop, and rendering stuff happens in the Panels framework, the actual game file for my comic is extremely simple. This is the entirety of my current `main.lua` file:

```lua
import "libraries/panels/Panels"
import "comicData.lua"

Panels.Settings.comicData = comicData
Panels.start()
```

I just import the framework, tell it where to find my comic data table and then hit `start()`. There are other settings one might want to change before starting the comic, but the defaults are pretty sensible.

---

# The Future

While my immediate focus is on finishing my own comic, I hope to make Panels publicly available around the same time.

I'm initially thinking of Panels as a developer tool. A developer would use the framework to build and publish their own comic for Playdate using the SDK tools provided by Panic.

At a later time it would be nice to create some more user-friendly tools to help generate the comic data without having to type it out by hand. There might even be some kind of generic "Comic Reader" app for Playdate where users can load data files and read comics without having to figure out the SDK tools to build their own app. I'll wait to see how much interest there is before starting on any of that.

In the meantime, I'd love to get some folks to try to use the framework and give feedback in the coming weeks. If you're interested in helping to beta test, let me know.
