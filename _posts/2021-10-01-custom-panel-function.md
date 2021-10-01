---
layout: post
title: "Custom Panel Functions"
tags:
  - code
  - panels
---

As I'm building [Panels](/2021/08/16/building-panels-framework/), I'm keeping things as flexible as possible. I need to accommodate all the different types of panels and animations I know I want to have in my comic, and I'm trying to anticipate what types of things others might want to do as well. I want to enable as much as I can, in the simplest ways possible.

But I know I'll never be able to anticipate _everything_ a person might want to do. And even for my own comic, it doesn't make sense to try to build an abstracted way to define complex panel behavior for something that will only be used once.

This panel is a good example:

![GIF](/images/posts/2021-10/adrift.gif#playdate)

I want the player to guide the character as he floats around the ship by tilting the device.

It would certainly be possible to build this functionality into the framework, but I don't think it's a common use case, and I imagine trying to define this scene in the comic data table would be cumbersome. You'd need to specify how each layer reacts to the tilt (or not), collision bounds, etc. And what if someone wants to add collectible items, enemy characters, or complex collideable objects? I'd much rather just be able to write this all out as a normal function where I can do whatever I want.

# Custom Functions to the Rescue

My solution is to allow any panel to specify a custom function that runs repeatedly while the panel is on screen. Actually, a panel can specify _three_ custom functions: A **render function** to handle all the logic and drawing for the panel, an **advance function** that determines whether the system should advance to the next panel or not, and a **reset function** that cleans up and resets the panel state if necessary. The render and advance functions get called every frame. The reset function only gets called once (when the panel leaves the screen). Resetting the panel state is necessary in case the user decides to navigate back to the custom panel.

Defining these functions in the comic data is as simple as listing them in the panel properties:

```lua
{ -- panel 6C
    renderFunction = renderPanel6C,
    advanceFunction = advancePanel6C,
    resetFunction = resetPanel6C,

    layers = {
        { image = "s06/C-1-wall.png" },
        { image = "s06/C-5-shadows.png" },
        { image = "s06/C-3-man.png" },
        { image = "s06/C-5-walls.png" },
    },
},
```

I still include the layers for this panel so the framework can handle loading and caching the images.

## Render Function

My render function gets passed the entire `panel` object, so I can access all the layers and any other properties of this panel. The function also gets the current scroll offset, which is what's typically used to compute layer parallax. In this case we'll use the accelerometer values instead.

Here's a stripped down version of the render function for the panel above:

```lua
local function renderPanel6C(panel, scrollOffset)
    if not playdate.accelerometerIsRunning() then
        playdate.startAccelerometer() -- turn on the accelerometer
    end

    -- read the tilt values and update the man's position
    local x, y, z = playdate.readAccelerometer()
    man.x = man.x + x
    man.y = man.y + y

    checkBounds(man) -- keep the man within the panel bounds

    for i, layer in ipairs(panel.layers) do
      -- calculate the tilt position of each layer
      -- and draw it to the panel
    end
end
```

Note that this function is responsible for drawing all the layers in the panel. If you need _some_ custom drawing or behavior in your panel then you become responsible for _all_ the behavior and drawing for the panel.

## Advance Function

In a manually scrolling sequence, the user can just keep scrolling past your custom panel. But in my case, I want this panel to stay on screen until the user navigates to the garden exit. My advance function indicates when this condition is met. Panels simply calls this function every frame to check if the advance condition has been met.

```lua
local function advancePanel6C()
    if man.y < -24 then
        return true -- ready to advance
    else

    return false -- stay on this panel
end
```

My `checkBounds()` function keeps the man from moving off the top of the screen unless he's within the exit door, so I simply check whether he's moved off screen or not.

## Reset Function

If the user navigates back to this panel, the advance condition will still be true, so they'll immediately advance again. To avoid this, I can reset the panel state in the reset function. This function gets called only once when the panel leaves the screen, so this is also a good place to kill any sound effects, timers or handle any other cleanup (like turning off the accelerometer).

```lua
local function resetPanel6C()
    man = {x = 16, y = 118} -- reset the man's position
    playdate.stopAccelerometer()
end
```

## Conclusion

I don't anticipate that this is something most comics will need to use very often (if at all), but it's nice to have a built in method for ejecting a panel's entire logic and rendering to a function where I have total control.
