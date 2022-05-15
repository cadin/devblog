---
layout: post
tags:
title: Illumination and Panels 1.0 Launch
---

I published my mini-comic [_Illumination_ on Itch](https://cadinb.itch.io/illumination) this weekend.

<iframe frameborder="0" src="https://itch.io/embed/1523251?bg_color=313029&amp;fg_color=c6c6c4&amp;link_color=FEC832&amp;border_color=313029" width="100%" height="167" style="border-radius: 8px;" ><a href="https://cadinb.itch.io/illumination">Illumination by Cadin Batrack</a></iframe>

I decided to make the game free to download for three reasons:

1. I want to be able to use this game as an example for people trying to use [Panels](https://cadin.github.io/panels/) to make their own comics. I put the [source up on GitHub](https://github.com/cadin/illumination) for folks to reference. I've been thinking about making some tutorial videos for Panels as well, in which case I can use this game as the source material.

2. I want to have a demo of a Panels comic that has enough in common with [_The Botanist_](https://cadinb.itch.io/the-botanist) that people can try it out for free to help them decide if they want to pay for the larger comic.

3. The play time of the comic ended up being incredibly short (about 2-3 minutes), despite it taking a lot of time and effort to produce. I don't want to deal with people whining about the price. Hopefully having this free demo will reduce the amount of whining about paying for _The Botanist_ when it comes out.

So far I've gotten a lot of good feedback about the game, and possibly some new interest in Panels, though I've yet to see anyone take a serious crack at making their own comic.

# Panels 1.0

Working on this game was a good stress test of my Panels framework. I fixed a few minor bugs along the way, and feel pretty confident about merging all my recent changes into a [1.0 release](https://github.com/cadin/panels/releases) now that I've been able to test on device for a bit.

### Reduce Flashing

I did add one new feature to the framework as a result of working on this new comic. In one of the panels I have a large dark layer that blinks of and on very rapidly. I wanted to provide a slower blink rate for users that have Playdate's Reduce Flashing setting enabled. So I added a `reduceFlashingDurations` option to the [`BLINK` layer effect](https://cadin.github.io/panels/docs/comic-data/layers/effects.html#blink) that will be used in these cases (otherwise the default `durations` timings will be used).
