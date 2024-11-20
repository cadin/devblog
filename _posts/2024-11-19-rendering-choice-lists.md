---
layout: post
tags:
title: Displaying Choice Lists in Fauna
---

_Fauna_ is a non-linear story, so the player needs to make choices at several points to determine the story path.

![Screenshot of a story point where the user visually selects an item to order for dinner](/images/posts/2024-11/DinnerDasher.gif#playdate "A graphical decision screen")
{:.tofigure}

Sometimes these decision points are something graphical or interactive like selecting which door to open, or branching based on the outcome of a mini-game, but they are often just choosing from two different text options.

I think it's helpful to try to always draw these in the same style so they are recognizable and it's clear to the user when they need to make a choice to move the story forward. I'm choosing to draw my options as large buttons with a little Mickey hand pointing to the selected option.

![Screenshot of two buttons with one selected](/images/posts/2024-11/textChoice.gif#playdate "A simple text choice")
{:.tofigure}

They are quite simple, but it's kind of pain to draw these in Panels. It's currently not possible to do this without using [custom functions](https://cadin.github.io/panels/docs/comic-data/custom-functions.html).

# My Current Approach

My current approach involves:

- a `Panels.vars` variable to indicate the currently selected item. I'll also use this variable in the future to determine the story path or render different elements based on the user's choice here.
- a custom `updateFunction` to handle button presses (usually just up and down). These inputs change the value of the variable mentioned above.
- a custom `renderFunction` to draw the buttons and hand pointer based on the current value of the variable.

After building this out just a couple times I realized I needed to make it easier on myself, so I extracted the [button rendering code](https://gist.github.com/cadin/acf4f9eac288faae8fa9b41d045fefdc) into a separate global function that I can call to draw buttons in any of these panels.

Even so, I still end up with something like this every time I want to render a choice list in a panel:

```lua
-- set the `didCrowMission` variable based on user input
local updatePanelC = function()
    if playdate.buttonJustPressed(Panels.Input.UP) then
        Panels.vars.didCrowMission = true
    elseif playdate.buttonJustPressed(Panels.Input.DOWN) then
        Panels.vars.didCrowMission = false
    end
end

-- render the list of choice buttons based on the current state
-- of the `didCrowMission` variable
local renderPanelC = function(panel, offset)
    -- draw other layers in this panel if needed

    renderChoiceList(
        {"Climb up to meet crows", "Go get food"},
        50, 50, 280, 40, -- x, y or list; w, h of each button
        Panels.Color.WHITE,
        Panels.vars.didCrowMission and 1 or 2
    )
end

-- tell the comic which sequence comes next
-- based on the `didCrowMission` variable
local targetSequencePanelC = function()
    if Panels.vars.didCrowMission then
        return "ladder"
    else
        return "deciding-on-food"
    end
end
```

# A Simpler Method

One could probably simplify this slightly by using layers with [conditional rendering](/2024/10/29/conditionally-rendering-images/) for the highlighted buttons and pointer hand. Then you wouldn't need to use the render function, as everything would be defined in the comic data.

I do similar things in some of the more graphic panels, but for text-only choices I like the flexibility of not having so much of it baked into images.

# Building it Into Panels

Whenever I find myself repeatedly writing boilerplate code like what I have above, I want to abstract it and centralize it. This is probably something that should be built into the Panels framework. I've hesitated to try to do that because I think it would be difficult to do it in a way that makes it easy for people to customize the look of their buttons, fonts, etc. And I don't know if it would be worth that effort since I haven't seen anyone else trying to build branching comics in Panels (yet).

But ideally you'd be able to write the choices directly into your comic data:

```lua
{ -- panel data
    layers = {
        {
            choices = { "Climb up to meet crows", "Go get food" },
            variable = "didCrowMission",
            values = { true, false }
        }
    }
}
```

That would remove all the custom functions except still needing a way to set the target sequence based on the variable. That could easily be added to the sequence data:

```lua
sequence01 = {
    targetSequence = {
        variable = "didCrowMission",
        values = { "ladder" = true, "deciding-on-food" = false }
    }
}
```

I could render the buttons with some default styling and fonts and let the user change it with some global settings.
And of course you could always fall back to using custom functions if you run into a case where the built-in system doesn't meet your needs.

I'd be interested to hear from anyone who might use a feature like this. How would you want it to work? You can give me feedback in the [Fauna devlog thread](https://discord.com/channels/675983554655551509/1294800080091484190) on the [Playdate Squad Discord](https://discord.gg/H6r4wyT5).
