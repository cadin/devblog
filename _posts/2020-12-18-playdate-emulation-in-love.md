---
layout: post
tags:
  - love2d
  - tools
  - code
title: Playdate Emulation in LÖVE
featured: false
carousel: ""
---

I created a small template project for previewing my [Playdate](https://play.date/) prototypes built with [LÖVE](https://love2d.org/) in a Playdate-like environment.

I don't yet have access to the Playdate SDK, so I'm not trying to mimic how any of that actually works. I just want a way to view my prototypes on the Playdate screen, so I can see them in the context of the device. This includes showing the project on top of an image of the Playdate console, and rendering everything in the style of the device's 1-bit LCD screen.

![Playdate emulation in action](/images/posts/2020-12/playdate-device.png)

The main part of the project (in `main.lua`) loads the image of the Playdate console and creates a separate [Canvas](https://love2d.org/wiki/Canvas) for rendering the game. The LÖVE functions for `update` and `draw` in this file call into corresponding functions in the `game.lua` file. This way I can put all my game code in the game file and keep it mostly separate from the Playdate emulation code.

The only somewhat fancy thing happening is this shader to mimic the LCD screen:

```glsl
lcdShader = love.graphics.newShader[[
vec4 effect( vec4 color, Image texture, vec2 texture_coords, vec2 screen_coords ){
    vec4 pixel = Texel(texture, texture_coords );
    if(pixel.r < 0.65) {
        return vec4(0.193, 0.184, 0.158, pixel.a);
    } else {
        return vec4(0.747, 0.757, 0.743, pixel.a);
    }
}
]]
```

This shader gets applied to the canvas that I use to render the game. It runs a simple threshold to determine whether a pixel should be "black" or "white" and colors it light gray or dark gray to mimic the look of the LCD screen. This way I can load true 1-bit black and white graphics, smooth anti-aliased images, or even full color photos, and everything gets displayed close to how it will actually appear on the device.

I also added a toggle to display the project by itself (without the device image) at 1x or 2x scale. This lets me get an up-close look at those chunky pixels.

![Project-only view](/images/posts/2020-12/playdate-window.png)

## Project Repo

This project is free for anyone to use on GitHub, though it will hopefully become obsolete soon when the official SDK is released.

Find the repo here:  
**[love-playdate-emulation](https://github.com/cadin/love-playdate-emulation)**
