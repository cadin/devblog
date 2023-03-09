---
layout: post
tags:
title: Making a Video Trailer for "The Botanist"
---

I created a short video trailer for _The Botanist_:

<video width="100%" controls poster="/images/posts/2022-06/botanistPoster.png">
<source src="/images/posts/2022-06/botanistTrailer.mp4" type="video/mp4">
</video>

I wanted to have a video to show off some of the animation and gameplay elements that don't come across in static screenshots. Even in screen captures of the game, it's difficult to tell how exactly things are reacting to the controls. Having the _[Illumination](https://cadinb.itch.io/illumination)_ demo will helps with this, but I wanted to capture video of someone actually playing through different parts of the comic.

---

## Recording the Playdate

I wanted to record gameplay directly on the Playdate screen.

I built a high-tech stand for my Playdate to try to keep it steady during filming. This consisted of some Silly Putty stuck to a tea tin. This elevated the device enought to let me grip it and manipulate the crank, without letting it wobble and drift so much that it moved out of focus.

![Playdate stand](/images/posts/2022-06/playdateStand.png "An old tea tin elevates the Playdate and keeps it steady. A bit of Silly Putty holds it in place.")
{:.tofigure}

## Screen Jitter

The comic runs at a pretty consistent 25 frames per second, which looks perfectly smooth in person, but causes a lot of ghosting and jitter on camera when mashed up with the camera's own frame rate.

![Example of frame ghosting on the Playdate screen](/images/posts/2022-06/frameGhosting.png "A ghosted portion of the previous screen state is captured in this single video frame")
{:.tofigure}

In a more traditional game this might not be an issue, but since my comic is constantly scrolling large full-screen graphics it was very noticeable and unpleasant. I tried a few different setups and frame rates, but could never get anything that looked acceptable, so I ended up capturing screen recordings through the Playdate simulator and compositing them into the live footage.

To match the color balance of the live footage, I captured the gameplay from the simulator in black and white and colorized the footage to match the LCD colors in the live footage. I did this in After Effects by using the black and white footage as a luminance matte for some colored solids.

And even with my fancy device stand, there was still a bit of wobble in the live footage, so I had to motion track the screen corners in the footage and map the screen captures onto the device screen.

![Motion tracking the live footage in After Effects](/images/posts/2022-06/motionTracking.png "'Perspective corner' tracking in After Effects to compensate for device motion in the live footage")
{:.tofigure}

This all ended up being a lot more work than I was anticipating, but in the end I think the video came out looking pretty good.

The video is [posted on YouTube](https://www.youtube.com/watch?v=6aiAtscy5Bs) if you'd like to share it.
