---
layout: post
tags:
title: Planning a Choose-Your-Own-Adventure Story
---

Creating a choose-your-own-adventure story is really fun, but it can easily get out of hand if you haven't planned ahead and prepared for all the branching paths your story will take. In the simplest version, each time your reader is asked to make a choice, the story branches off into two (or more) new paths. With this approach, you'll quickly end up with an unmanageable number of story paths to write, keep track of, and (in my case) draw images for.

![Illustration showing many branches creating an exponential number of story paths ](/images/posts/2024-10/exponential-map.png "After just four levels of choices, I already have 16 storylines to manage")
{:.tofigure}

In my experiences reading choose your adventure books when I was younger, it seemed like they often solved this problem by creating one or two "main" storylines, where many of the other branches lead to a dead end. I always hated this because it made me feel like I'd chosen wrong, and I needed to backtrack to get back on what the author had decided was the correct story path. Ideally, any choice the reader makes should result in a story path that feels as long, eventful, and meaningful as any other.

![Illustration showing one main trunk with short dead end branches coming off of it](/images/posts/2024-10/limited-map.png "Only one path leads to a long fulfilling story")
{:.tofigure}

# Guardian Quest

Several years ago I worked on a Flash game called _Guardian Quest_ with a choose-your-own-adventure storyline. In the development of this game I discovered two strategies to help keep the scope manageable: intersecting story branches and the diamond shaped story map.

## Intersecting Branches

In my illustration above, each time a story branches, it gets its own separate path, that in turn contains its own branches. Each choice multiplies the number of story paths exponentially. But it's possible to limit this infinite growth problem by having some of the branches rejoin the existing trunks. You can have a branch that diverts to take the reader on a side-quest, before rejoining the path they were on before, or have one of their choices take them to another location where they join a separate trunk that diverted earlier in the story.

![Illustration showing a story map with intersecting paths](/images/posts/2024-10/intersecting-map.png "Paths rejoin and intersect to reduce the total number of branches")
{:.tofigure}

Using this technique, you can create a story with many possible paths through it, without continuing to multiply the number of story branches.

Doing this requires a lot of up-front story planning, because you need to ensure that any time you rejoin an existing branch the story from that point on will make sense no matter which path you took to get there.

## The Diamond

It was this story planning process that led me to discover the diamond shaped story. In the diamond shape, the number of branches expands at the beginning and middle of the story, and then the branches start to rejoin and funnel back down to a limited number of endings.

![Game map for _Guardian Quest_, showing the diamond shape](/images/posts/2024-10/vermonia-game-map.gif "Game map for Guardian Quest")
{:.tofigure}

In this map for _Guardian Quest_, you can see I have the number of branches expands throughout the story, but they narrow down to just three possible endings. You can also see how closely intertwined the intersecting story paths are.

# Mitigating Repetition

One of the benefits of creating a choose-your-own-adventure story is that users can read through it multiple times. But if we're letting story paths rejoin and narrow down to just a few different endings, won't readers be frustrated by the repetition? I've found that even if a story only has a certain number of set endings, it can still feel satisfying to replay as long as there are a sufficiently large number of pathways to get to those endings.

Nevertheless, how can we mitigate this sense of repetition that readers might begin to feel?

## User Choice

The easiest answer to this is that the readers themselves will avoid frustration by just making different choices. If one notices that they've rejoined a story path they've already been on, they can simply divert at the next opportunity by making a different choice than they made last time. They'll have to play through many times before they start feeling like they've exhausted all their choices.

## Programmatic Tweaks

A huge benefit of creating the story as a digital game instead of a printed book is that we can make programmatic changes to a storyline based on the reader's past choices. They might be traversing the same story branch as a previous readthrough, but we can swap out images and dialog to make things feel tailored to their choices and keep their interest. We can also open different branches based on past choices, so making a choice early on not only determines the story branch that they take, but it can have impacts on the choices available to them much later in the story.

## Souvenirs

With digital stories, it's also possible to track the reader's journey through the story in a way that allows you to create a custom takeaway that's unique to that specific playthrough. In _Guardian Quest_, players were awarded a downloadable card that featured the unique animal guardian that had been revealed to them in the game. Their guardian was also decorated with a bespoke costume and jewels, and the card's text and graphics were customized based on how they performed on mini-games within the story, and how many secrets and collectible items they had found. This way, even if they played through the same story path, making the exact same choices, they would still receive a unique souvenir at the end of each game.

With today's print-on-demand services, you could even turn this into a physical item, so users could order a custom print, sticker, or t-shirt that represents their journey through the story.

# Fauna

The story I'm creating for _Fauna_ is much more complex than anything I've worked on before, but I'm trying to keep these past lessons in mind as I plan out the story map. I'm letting story branches intersect and cross over to other branches, and trying to narrow things down to just a few primary story paths at the end.

![Screenshot of the Fauna story map](/images/posts/2024-10/fauna-game-map.png "A small section of the Fauna story map")
{:.tofigure}

At this point, it's still feeling a little overwhelming, but I'm excited about where it can go.
