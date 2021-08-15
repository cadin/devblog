---
layout: post
tags:
  - code
  - playdate-sdk
title: Moving to the Playdate SDK
featured: false
carousel: ""
---

After I posted some of my comic progress on the unofficial [Playdate Squad Discord](https://discord.gg/YCZxgQGsZH) Neven was nice enough to offer me access to the real Playdate SDK (which is still in private beta). So I've been spending some time recently getting up to speed on the SDK and moving my code over from my LÖVE prototype to the official framework.

So far everything has been going smoothly, and I have most of the core functionality working in the Playdate simulator.

![Demo of my comic running in the Playdate simulator](/images/posts/2021-08/PlaydateComic.gif#playdate "Scrolling through the first sequence of my comic in the Playdate simulator")
{:.tofigure}

## Hiccups

Fortunately, I haven't really run into anything in the SDK that has hindered porting my code from the LÖVE prototype. Most of the things that hold me up are idiosyncrasies in Lua, not Playdate. I'm glad I took the time to get up to speed on Lua by prototyping a bit before getting into the SDK. It makes it all seem less overwhelming.

I wasn't able to figure out how to get a good build-and-run system working in my preferred editor (VS Code), so I'm using [Nova](https://nova.app) for now which (of course) has great Playdate integration. Maybe when the SDK is public someone will build something nice for VS Code that I can use.

## Hardware

The only real pain point I'm feeling right now is not having access to a device. The simulator is really great, but not being able to actually feel crank-scrolling through the comic makes it difficult to gauge things like scroll speed and panel snapping thresholds. All of that is easy enough to fine tune once I get my hands on one though. On-device performance is the other big unknown at this point. I'm not doing anything too processor intensive, but I'm not sure how the hardware will react to me constantly doing full screen redraws. I'll hold off on trying to optimize anything until I have a device to test with.
