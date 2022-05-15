---
layout: post
tags:
title: Optimizing Audio for Hardware Playback
---

I got my Playdate today!  
Of course I wanted to immediately load up The Botanist to try it on the actual hardware.

![Playdate device running The Botanist comic](/images/posts/2022-04/hardware.jpg)

I was happy to find that overall it looks great on the device. The Playdate screen has a really unique quality. It almost feels like looking at printed paper.

As I started moving through the comic I found that a lot of the scrolling and animations were quite choppy. I was expecting to have to do some optimizations for hardware, but I was kind of surprised at the performance because I had given an early version to some folks to test on device and they had all reported that it ran smoothly.

Progressing through the game, I also found that some sequences were not playing the background music, even though they played in the simulator. Strangely, it seemed that the sequences that played without sound also scrolled much more smoothly than the others.

## Don't Use MP3 Files

The SDK docs for [Fileplayer](https://sdk.play.date/1.10.0/Inside%20Playdate.html#C-sound.fileplayer) warn against using MP3 audio:

> Fileplayer can play MP3 files, but MP3 decoding is CPU-intensive. For a balance of good performance and small file size, we recommend encoding audio into ADPCM .wav files.

I knew about this, but chose to favor the smaller file sizes of MP3 until I got my Playdate to see if it would actually affect performance in my game. I'm surprised to see how much of an impact it can have.

So the first step was to swap out my background music MP3 files for ADPCM-encoded WAVs. I used [Matt's ADPCM encoder tool](https://devforum.play.date/t/adpcm-encoder-tool-mac-only/1283) which made this super easy.

## Playback Buffer

After swapping out the files, the scrolling looked much better, but now I didn't hear the background audio for _any_ of the sequences.

This one took much longer to track down. I could see that the files were getting loaded just fine, and calling `play()` returned no errors, but checking `isPlaying()` always returned false. I thought perhaps something in my code was inadvertently stopping the audio immediately after starting it, but everything still worked just fine in the simulator.

Finally I found this function in the docs that I hadn't noticed before:
**[playdate.sound.fileplayer:setStopOnUnderrun(flag)](https://sdk.play.date/1.10.0/Inside%20Playdate.html#m-sound.fileplayer.setStopOnUnderrun)**

> By default, the fileplayer stops playback if it can’t provide data fast enough. Setting the flag to false tells the fileplayer to restart playback (after an audible stutter) as soon as data is available.

I think because I start my background audio at the same time I'm loading up all the images for a new sequence and animating in the panels, it can't load the song fast enough and just halts playback. I was able to verify that this was what was happening by using [`setFinishCallback()`](https://sdk.play.date/inside-playdate/#m-sound.fileplayer.setFinishCallback) and checking [`didUnderrun()`](https://sdk.play.date/inside-playdate/#m-sound.fileplayer.didUnderrun) from there.

Setting the stop on underrun flag to false did make the audio play as expected, but I was worried that might cause stuttering when loading a particularly heavy sequence or animation. Instead I specified a larger `buffersize` when creating the fileplayer. I'm not sure what the optimal value here is. It looks like the default is 1/4 of a second. I set it to 2 seconds for now and everything seems to work perfectly. I may tweak that in the future as I continue to fine tune the Panels framework for hardware.
