---
layout: post
tags:
  - code
  - panels
title: Announcing Panels for Playdate
featured: yes
carousel: ""
---

![Banner with Panels logo](/images/posts/2022-03/panelsBanner.gif)

Now that the [Playdate SDK](https://play.date/dev/) is publicly available, I'm happy to be able to release my Panels framework. Panels lets you build interactive comics for Playdate with parallax scrolling, animated layers, synced sound effects, chapters and more.

Simply provide Panels with a Lua table that describes the sequences in your comic (scroll direction, panel sizes, text, animation and effects) along with your layered graphics. Panels will handle layout, scrolling, animation, and even chapter navigation for you.

## Important Links

### &nbsp; 🗄 [Panels code repo](https://github.com/cadin/panels)

### &nbsp; 📄 [Panels documentation](https://cadin.github.io/panels)

### &nbsp; 📦 [Panels project template](https://github.com/cadin/panels-project-template)

---

## Getting Started

The easiest way to get started is with the [Project Template](https://github.com/cadin/panels-project-template).

#### With Git

The template project includes the Panels framework as a git submodule. If you make sure [initialize submodules](https://www.w3docs.com/snippets/git/how-to-clone-including-submodules.html) when cloning the repo, git will pull the current version of the framework into your project.

#### Manual Setup

If you're not using git, you can download the project template code as a ZIP file. In that case you'll also need to download the code from the [Panels repo](https://github.com/cadin/panels) and place it in the `source/libraries/panels/` folder of the project template.

#### Start Building

Edit the table in `source/myComicData.lua` to start building your comic.

Edit `source/main.lua` to add [game credits](http://cadin.github.io/panels/docs/credits-screen) or alter [Panels settings](http://cadin.github.io/panels/docs/settings).

&nbsp;

## Examples

![Example comic](/images/posts/2022-03/example3a.gif#playdate)

The project template comes with a few simple examples built in. It's probably best to spend some time playing with these examples to get a feel for how the system works.

1 [**Simple Comic**](https://github.com/cadin/panels-project-template/blob/main/source/examples/1-simple-comic.lua)  
Create a series of panels with image layers with parallax scrolling.

2 [**Animation**](https://github.com/cadin/panels-project-template/blob/main/source/examples/2-animation.lua)  
 Set a layer to animate across the screen as the panel scrolls, or when the user presses a specific button.

3 [**Image Transitions**](https://github.com/cadin/panels-project-template/blob/main/source/examples/3-image-transitions.lua)  
 Transition between two images on the same layer based on panel scroll position, or button press.

4 [**Custom Functions**](https://github.com/cadin/panels-project-template/blob/main/source/examples/4-custom-functions.lua)  
 Create custom render, advance, and reset functions to take over drawing and behavior of a single panel.

5 [**Audio**](https://github.com/cadin/panels-project-template/blob/main/source/examples/5-audio.lua)  
 Play background audio for an entire sequence or a single panel. Trigger a sound effect synced with an animation.

&nbsp;

## Preview

I've been using Panels to build my own comic called _The Botanist_, a sci-fi story about a scientist traveling the galaxy searching for rare plants. This sequence shows a little more of what's possible when you dig into all the features of the framework.

![Animated comic of shuttle launching](/images/posts/2022-03/shuttleLaunch.gif#playdate)
