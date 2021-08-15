---
layout: post
tags:
  - art
title: Pixel Art Workflow
featured: false
carousel: ""
---

I've made some adjustments to my drawing workflow to make it a bit easier and faster to produce artwork for my comic.

# The Old Way

The first few panels I made started as high-resolution drawings in Procreate. I would then bring them into Photoshop, resize them for the Playdate screen, and export the layers to be imported into the game.

![Old workflow](/images/posts/2021-08/workflow-old.png "You don't know exactly how the art will look until you see it in the game")
{:.tofigure}

I wanted to do the drawings in Procreate because I am very familiar with it and really love it. I also want the drawings to retain a certain amount of the hand-drawn aesthetic. I was worried that going straight to pixel art would look too computery.

I also thought it would be nice to start with high-res drawings in case I ever decided to recreate the comic in a different format (like print or web).

## Shortcomings

Starting with high-resolution drawings makes it really hard to get a sense of what the finished drawing will look like when it's downsampled and aliased. I spent a lot of time rendering certain details that didn't read in the final form, and some of the "hand-drawn" qualities that I wanted to preserve just ended up looking sloppy after conversion.

The fact that there are so many steps involved to get from the image I'm drawing to a representation of the image on device was very inconvenient. I couldn't find a good way to generate a 1-bit version of my drawing on my iPad, so I had to send the image to my Mac in order to process it in Photoshop.

If I didn't like what I saw, I'd end up going back and forth between devices and apps multiple times. The feedback loop was too long and cumbersome.

# The New Way

To try to make things more efficient I've been trying out a pixel-art app called [Pixaki](https://pixaki.com).

I still start with a sketch in Procreate in order to capture some hand-drawn qualities, but now I work at Playdate resolution (400 x 240) from the beginning. Starting at the smaller size means I remove the step of resizing later, and it helps me get a sense of how much detail I can put into the image from the time I'm first drawing it.

![New workflow](/images/posts/2021-08/workflow-new.png "Working in Pixaki gets me closer to the final image earlier in the process")
{:.tofigure}

From there I take the sketch into Pixaki and "ink" it with pixel brushes. The Pixaki app has a lot of room for improvement, but so far it's the best iPad pixel art tool I've found. The main thing I miss from working in Procreate is being able to control the brush size with pen pressure. Without that I have to manually swap brush sizes very a lot.

I still end up going to Photoshop on the Mac to merge and export layers, but I've removed the most annoying part of having to go and back forth repeatedly to make changes, since I can see what the finished art will look like as I'm working in Pixaki.

The one big thing I've lost in the change is having high-resolution original drawings. If I'm being honest with myself, I probably wouldn't have done anything with them anyway, so I'm not too worried about it. In the future I'll most likely prefer to spend my time creating a new story rather than reproducing the same one in a new format.
