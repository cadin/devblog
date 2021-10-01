---
layout: post
title: "Developing for Playdate in VS Code"
tags:
  - code
---

I created a template repo on GitHub with my VS Code setup (for Mac) that lets me build and run my project in the simulator:

### [Playdate VS Code Template](https://github.com/cadin/playdate-vscode-template)

---

## Nova

When I started developing with the Playdate SDK, I tried out Panic's [Nova editor](https://nova.app). It's a very nicely designed native Mac app. I expected to like it more than VS Code, which I only reluctantly adopted a few years ago because it's the tool we use at work. But when working in Nova I found myself being constantly slowed down by the minor differences from what I'm used to.

I tried a few times to get set up developing for Playdate in VS Code. This [Playdate extension](https://marketplace.visualstudio.com/items?itemName=Orta.playdate) in the VS Marketplace seemed outdated and didn't work. Tinkering around in the `settings.json` and `tasks.json` got me to where I could build a project, but I couldn't figure out how to automatically launch the simulator. (Nova of course has excellent integration with the Playdate simulator.)

I finally found an old post on the Playdate Discord where [Dovuro](https://twitter.com/Dovuro) posted examples of his VS Code config files. They looked too simple to actually be the answer I had been searching for, but lo and behold they worked—no extension or complex setup required. My template is based on his files.

## Old Friend

Now that I'm back in VS Code, I'm surprised to find that autocomplete for the Playdate SDK actually seems better than in Nova. In Nova, typing `playdate.graphics.` will bring up autocomplete suggestions for _everything_ in the SDK, instead of just the things in the "graphics" module. VS Code does this properly, and also provides suggestions for code in my own modules, which I didn't seem to be getting in Nova.

_And_ I can finally once again select a keyword in my code and see all other instances highlighted. I never realized how much I rely on that feature until it was missing. It seems strange that Nova doesn't have this. Perhaps I just couldn't find the setting to enable it.

I do look forward to trying Nova again once it's gotten a bit more mature.