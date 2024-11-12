---
layout: post
tags:
title: Conditionally Rendering Images in Panels
---

In a Panels comic you can use [custom functions](https://cadin.github.io/panels/docs/comic-data/custom-functions.html) to make your comic more interactive. That can be a complex [renderFunction](https://cadin.github.io/panels/docs/comic-data/custom-functions.html#render) that takes over from Panels and handles all the rendering for a specific panel, or a simple [updateFunction](https://cadin.github.io/panels/docs/comic-data/custom-functions.html#update) that deals with user input or some custom logic outside of the actual rendering. You can use those custom functions to set and read [variables](https://cadin.github.io/panels/docs/comic-data/variables.html) in order to create a dynamic panels that display different text or graphics based on the player's past behavior.

For example, I could have a custom render function that runs a mini game in a panel. The next panel can have its own custom function that reads the outcome of that game and changes to display a graphic that represents a win or lose state.

## Old

Currently, the only way to conditionally display an image like that is to use a custom render function. That means your code needs to take over rendering the panel and draw the correct images based on the game state. I've made that a bit easier with recent updates, where you can now pass off each layer to Panels to do the parallax calculations and rendering after performing any necessary logic.

That might look something like this:

```lua
local function renderPanel2(panel, offset)

    -- loop through all the layers in the panel
    for i, layer in ipairs(panel.layers) do

        -- display the locked or open door
        -- depending on whether or not the user has the key
        if (layer.name == "lockedDoor" and Panels.vars.hasKey == false)
            or (layer.name == "openDoor" and Panels.vars.hasKey == true) then

                -- pass the layer off to panels to render with parallax, etc
                Panels.renderLayerInPanel(layer, panel, offset)
        end
    end
end
```

## New

That method works just fine in a one-off panel, but quickly becomes cumbersome if you want to do conditional rendering in many panels throughout your comic. So I've been working to make it possible to do this kind of conditional rendering without needing custom functions by adding a `renderCondition` property directly to a layer in the comic data.

I currently have this:

```lua
layers = {
    { image = "s2/lockedDoor", parallax = 0.3,
        renderCondition = { var = "hasKey", value = false } },
    { image = "s2/openDoor", parallax = 0.3,
        renderCondition = { var = "hasKey", value = true } },
},
```

In the `renderCondition` table I just need to provide the name of the variable, and the expected value. If the provided value matches the current value of the variable, the layer will be rendered, otherwise it will be skipped. Any layer without the `renderCondition` property gets rendered as it normally would.

This makes it really easy to set layers to render conditionally without having to set up a complex render function for every panel. I also just like that it keeps all the logic in the comic data in an easy to read format.

# Coming Soon

This change currently exists on the [Panels dev branch](https://github.com/cadin/panels/tree/dev). I'm planning to push it with some other changes to an upcoming Panels 2.0 release.
