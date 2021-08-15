---
layout: post
tags:
  - art
  - love2d
title: Scrolling Comic Test
featured: false
carousel: ""
featured: 
---

I pulled together a test of a scrolling comic using my [LÖVE template](/posts/2020-12-18-playdate-emulation).

<video src="/images/posts/2021-07/PlaydateComicTest.mov" width="100%" height="auto" autoplay="true" loop="true" ></video>

This demo is just showing the same panels in two different sequences to let me test some of the features I want the system to have:

- layered, parallax scrolling
- nested panels
- different scroll directions per sequence
- panel effects like shake and blink
- animated transitions between sequences
- animations and transitions within panels based on scroll position

## Artwork

All of the artwork here was drawn hi-res in Procreate, and then downsized. The 1-bit conversion happens with the shader built into the LÖVE template.
I'm not that happy with how these panels are looking, and this workflow is a bit too cumbersome. I'll need to figure out a better process for making these drawings.

## Framework

My hope is to build the framework for this abstract enough that it will be relatively easy to create new comics by populating images and a data file. Might even be something that others could use to create their own stories.
Keeping these different concerns organized and separate from each other has been the biggest programming challenge so far.
