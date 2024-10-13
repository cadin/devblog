---
layout: post
tags:
title: "Multiplayer Combat on Playdate"
---

The [Playdate](www.play.date) doesn't have a networking API, so if you want to make a multiplayer game you'll be limited to some kind of analog solution. Pass-and-play is a good option for playing with someone in the same room, but what about a system where you could play with someone on the phone or online without needing to physically pass the device back and forth?

[Chess can be played like this](https://en.wikipedia.org/wiki/Correspondence_chess). Each player just tells the other which move they're making, and both players keep an up-to-date version of the board. What kind of games could we make for Playdate using a similar kind of system?

## Ace of Aces

![Ace of Aces game set](/images/posts/2024-09/AceOfAces-Game.png "Photo by Hilmar Carders - From Wikipedia")
{:.tofigure}

In the 80s there were a series of "game books" called [_Ace of Aces_](<https://en.wikipedia.org/wiki/Ace_of_Aces_(picture_book_game)>). In these two-player games, each player holds a small booklet in which each page shows a different first-person view looking out from a plane cockpit. Players start with a view of the enemy plane in the distance and must maneuver their planes into a position where they can attack the other player. The possible moves are listed at the bottom of the page. Players choose their moves and tell the other player the page number associated with their move. Each player turns to the new page they've been given to see an updated view of the current dogfight.

This ingenious (and totally analog) system keeps the relative positions of the players' planes in sync while giving them each a unique view of the action.

## Digitizing

This gameplay system could lend itself nicely to a Playdate game.  
I made some rough concept images using scanned pages from the books to illustrate how it could work:

<div style="display: grid; grid-template-columns: 1fr 1fr;  gap: 1rem; margin-bottom: 1rem;">
<img src="/images/posts/2024-09/concept1.gif#pixel" class="playdate" style="border-radius: 4px"/>
<img src="/images/posts/2024-09/concept2.gif#pixel" class="playdate" style="border-radius: 4px"/>
</div>

Like in the books, each player starts the game with a view of their opponent. To take your turn, you choose your desired move from a list using the d-pad or crank.

<div style="display: grid; grid-template-columns: 1fr 1fr;  gap: 1rem; margin-bottom: 1rem;">
<img src="/images/posts/2024-09/concept3.gif#pixel" class="playdate" style="border-radius: 4px"/>
<img src="/images/posts/2024-09/concept4.gif#pixel" class="playdate" style="border-radius: 4px"/>
</div>

Once you've selected your move, the game gives you a code (could be a number or a letter) that you send to your opponent. The codes obscure your move, so your opponent can't base their move on what you did. When you get the move code from your opponent you input it into your Playdate and the view updates to show the results of both players' moves.

### Some Details

The codes associated with the moves would need to change each turn. Otherwise you'd quickly learn that for example when your opponent tells you to input "AA" that corresponds to a right turn. Whatever system is used to randomize the move codes needs to be something that can be synchronized across both Playdates.

The mechanism for choosing a move could be made more dynamic and fun by using the d-pad to choose a direction and speed instead of choosing a distinct move from a list. At the very least, the moves could be more clearly labeled or illustrated compared to the somewhat cryptic symbols in the game books.

## Pros and Cons

A lot of the fussier aspects of the analog game books could be improved by moving to a digital game system.

In the original game, players needed to navigate to two separate pages for each turn. First, you'd turn to the page number given to you by your opponent. This reflected the _opponent's_ move. From this page, you'd look up the page number associated with _your_ move and turn there to see the fully updated game state. In a digital version, the game logic can handle the intermediate logic behind the scenes. The player just needs to input their move and their opponents move and they get the updated view.

In the books, of course each view is a static drawing of course. The Playdate view could show some subtle movement and sound effects to make the static views more interesting. And when the moves are input, the planes could animate into their new positions instead of just switching to a new static image.

On the Playdate, you could have multiple saved games going at once against different opponents. You could switch over to a different game while you wait for your opponent to make their move.

I think this could be a made into a great game for the Playdate. I hope someone makes it! But there were two reasons that I decided not to pursue the idea myself:

**One**, the sheer amount of drawings needed is overwhelming.

In _Ace of Aces_ there are hundreds of of different views in _each book_. They need to be drawn with enough detail and accurate perspective so that you can get a good sense of your opponent's position. If you wanted to add different types of planes for the players to choose from, you'd need to create a whole new set of images.

This could all be greatly simplified if you were to create the images in 3D, instead of drawing them manually. Then you'd just need to render out the images for each view without redrawing it each time. You could even do some fun animation of the planes moving into the new view when the players's moves are locked in. I'm not a 3D artist, so all of this is outside of my skillset.

And **two**, the magic of the system gets a bit lost when you're doing it on a handheld computer instead of a printed book.

A huge part of the charm of the _Ace of Aces_ games is that it's all happening in an analog book. It really feels like magic to be having a synchronized dogfight battle just by flipping around through pages in a book. I worry that some of this charm will be lost when you're doing on an actual computer. Will it still be magic, or will it just feel clunky and slow?

## Expanding the Idea

If someone does pick up this idea, there are a ton of ways to take it further than just reproducing the _Ace of Aces_ game.

You could program a simple AI opponent to make it possible to play a single-player mode against the computer.

You could also make games that aren't just planes dogfighting. They could be spaceships or racecars or tanks. Some of the old game books even tried things like [western shootouts](https://boardgamegeek.com/boardgame/3089/bounty-hunter-shootout-at-the-saloon) and [dragon battles](https://boardgamegeek.com/boardgame/5735/dragonriders-of-pern-the-book-game).

![Dragon Riders Page](/images/posts/2024-09/dragon.png "“Dragonriders of Pern” Game Book - from BoardGameGeek.com")
{:.tofigure}

You could have players choose which planes (or ships) to fly at the beginning of a battle. The different ships would have different graphics of course, but might also be able to perform different moves, have more powerful weapons or stronger defenses.

## Mechanics

To actually build a game like this you'll need to understand the mechanics behind it.

This archived article does a great job of explaining how the game works, and how the player's views are calculated based on their relative positions:

**[GameTek #4: All About That Ace](https://web.archive.org/web/20210717161613/https://www.getrevue.co/profile/gengelstein/issues/gametek-4-all-about-that-ace-680928)** by Geoff Engelstein (archived)

The game state can be modelled with a hex grid, where the player's relative positions can be mapped to show each plane's view and the corresponding page number.

![Hex grid](/images/posts/2024-09/hexGrid.png)

I still find it fascinating that someone was able to figure out how to make this all work.

For a nice bonus, check out this video of the creator Alfred Leonardi teaching his grandkids how to play: [**Ace of Aces Tutorial** on YouTube](https://www.youtube.com/watch?v=UF8BF7_ywkI)
