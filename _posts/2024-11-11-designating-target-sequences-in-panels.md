---
layout: post
tags:
title: Improved Sequence Targeting in Panels
---

A while back I added some [basic functionality](https://cadin.github.io/panels/docs/nonlinear-comics.html) to support branching stories in Panels. Now that I'm actually using it, I'm finding a few ways to make it easier to work with.

# Target Sequence

In a linear comic, you just give Panels a list of sequences and the user plays through them in order. But when the comic contains branching choices, you need to somehow tell Panels which sequence to go to when the user makes their choice.

## Target Index

My solution for this was to add a `target` property, where you can specify the _number_ of the sequence where the user should go for the given action. This made a lot of sense because the sequences all come in as an ordered list, and in the Panels code I navigate between them by referring to their order in that list.

![Illustration showing the difference between a linear list of sequences and a list where the user can jump to a sequence out of order](/images/posts/2024-10/sequence-targeting.png)

This _seemed_ to work fine because my test project---like my illustration above---contained very few sequences. It was easy to figure out the index of a sequence in the list and with only a few branches in the project, maintaining them was no problem.

In practice, this turns out to be very difficult to manage. My [new project](/2024/10/12/fauna/) already has many, many sequences. It's a pain to have to keep going back to my sequence list to find the index of the sequence I want to target. And maintaining them is a nightmare. If I ever decide to insert a sequence somewhere earlier in my project, it throws off all the indexes, and I have to go through the entire project and update all the targets.

## Target ID

A simple change makes this all much easier. Instead of specifying the sequence _number_ as the target, I can give my target sequence an ID (any unique name), and add that as the target value. Index number still works, but ID is much easier to deal with. They can be made more semantically meaningful and memorable, and they don't change when my sequence order changes.

### Example

All I need to do to make this work is give my target sequence an `id` property:

```lua
seq55 = {
	id = "fight-the-dragon",
	panels = {
		-- etc...
	}
}
```

And then any time I want to target that sequence I just set that ID as the `target` for an [advance control](https://cadin.github.io/panels/docs/comic-data/sequences.html#advancecontrols), or a [custom function](https://cadin.github.io/panels/docs/comic-data/custom-functions.html#target-sequence)

```lua
advanceControls = {
    { input = Panels.Input.A, target = "fight-the-dragon" },
    { input = Panels.Input.B, target = "run-away" },
},
```

# Coming Soon

This change currently exists on the [Panels dev branch](https://github.com/cadin/panels/tree/dev). I'm planning to push it with some other changes to an upcoming Panels 2.0 release.
