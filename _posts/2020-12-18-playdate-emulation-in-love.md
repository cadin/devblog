---
layout: post
tags:
- love2d
- " tools"
nouns:
- Deneba
- artWORKS
- HyperCard
- Macintosh
- System 7
- Playdate
- BasiliskII
- File Sharing
- iPad Pro
- iPhone
- AirDrop
- Apple Pencil
- Memphis Group
- DeBabelizer
- Photoshop
- Thoru Yamamoto
- Files
- iPadOS
- Twitter
title: Playdate Emulation in Löve
featured: false
carousel: ''

---
I created a small template project for previewing [LÖVE](https://love2d.org/) games in a [Playdate](https://play.date/)-like environment.

The main part of the project (in `main.lua`) loads the image of the Playdate console and creates a separate [Canvas](https://love2d.org/wiki/Canvas) for rendering the game. The LÖVE functions for `update` and `draw` in this file call into corresponding functions in the `game.lua` file, so you can put all your game code in the game file and keep it separate from the Playdate emulation code.

The only somewhat fancy thing happening is this shader to mimic the LCD screen:

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