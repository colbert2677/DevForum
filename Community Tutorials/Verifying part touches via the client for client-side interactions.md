Source: https://devforum.roblox.com/t/verifying-part-touches-via-the-client-for-client-side-interactions/359133

___

Every now and again, a question pops up on Scripting Support regarding handling part touches from the client. Two points are usually raised in these threads: the events are supposedly replicating despite being connected from the client, or that everyone's seeing client-connected events.

The intention of this thread is to clear the air about client-based part touch detections, look into some explanations and hopefully provide some useful knowledge.

Before you jump in...
=

There is an expectation that you have some knowledge about some key terms raised while going through this thread. There are terms such as *event*, *client* and *replication* used which may not be fully understood by new developers. Make sure to search for what you don't know!

At the time of writing, there are no links attached for any items or references in this article. This is to avoid a mass of blue text taking away from the writing. Once again: *make sure to search for what you don't know!*

___

What is Touched?
=

Touched is a physics-based event that is fired whenever two BaseParts come into contact with each other. In respect to it being based on physics, this means that one of the parts must be physically simulated. A part enters physics simulation when it is not anchored. CFraming is not physics simulation and CFraming parts into each other will not fire Touched!

In a typical scenario, you will usually use Touched to determine when two parts make contact so you can set up events that happen at the time. One of the most common use cases for Touched is to set up player interaction. For example, when you walk up to a booth, you want the player to see a shop. This is a relevant example for later so keep this in mind.

This event is part of the BasePart class, which means that *any* kind of part can have functions listen to when this event fires. Here's an comprehensive list of BaseParts you can use Touched with in alphabetical order:

- CornerWedgePart
- FlagStand (deprecated; was an engine-managed object for CTF games)
- MeshPart
- Part
- PartOperation (Unions and Negations) (for Blender users, equivalent of a BooleanOperation)
- Platform
- Seat
- SkateboardPlatform
- SpawnLocation
- Terrain (surprisingly, yes, Terrain can be touched!)
- TrussPart
- VehicleSeat
- WedgePart

Where can Touched be used?
=

Touched can be used anywhere at any time. Both the server and the client are able to have functions listen to when Touched fires. Be wary of their respective limitations however! Replication and script locations are very important to remember. The server cannot use Touched for a part created by the client, but both the server and client can use it for server-created parts. LocalScripts also only run in very specific places, which are specified on its documentation page.

Depending on your use cases and regard for performance and efficiency, this may change where you're using Touched from. A lot of users have opted to or have been recommended to use the client to listen to Touched for various actions such as showing a shop Gui. That's where this thread enters.

Why use Touched on the client?
=

Several points have been raised above which provide a basis for why you might be using Touched on the client, or rather why you should be. Let's look over those again briefly.

- *Physics-based:* The client can run things faster than the server can. When it comes to physics you want accuracy, near-instantaneous feedback and less strain on the server to prevent lag. With this in mind, you'll want the client to do what it can.

- *Replication:* A part may be created by the client and you may want to detect touches on it. The server will not be able to see this part, so the only answer is to have the client handle it!

- *Performance:* As stated in the first point of physics, you'll want to hold the server from handling small actions that the client can do, especially if they hold no importance and the action is ultimately only relevant to the client.

In addition to these three points, there is one that hasn't been addressed: networking. Let's summarise that similarly to the points above and then break it down.

- *Networking:* When you involve remotes, you start piling up network traffic. For Touched and Humanoids, the event could easily fire off many times and you could end up sending a huge amount of traffic to the client where not necessary.

When looking to fix issues with Touched events and the clients, there are often developers who recommend using remotes. The server listens for Touched and if it is able to find a player, then it sends a signal to them via a remote. This over using the client alone is bad in many ways. Here are two.

- *Traffic:* As stated above, you could potentially rack up several tens of requests unnecessarily to the client. This slowly leads into an programming anti-pattern called a code smell. Anti-patterns move from a problem to a bad solution; a code smell is indicative of weak structure. Code smells are *not* bugs and don't harm functionality, but they can slow down development.

- *Oversights and traps:* The mindset of needing the server to interface all world interactions can be carried over into other works where doing so is not necessary. It's also easy to get led into code oversights and in some cases, tank on maintainability. Whereas you can have two scripts with a network bottleneck, you can have one script or a chunk in a larger script that handles the entire workflow for the touch event.

How do I use Touched on the client?
=

There's only one way to have a function listen to the Touched event. The same way you'd do it for the server works for the client as well. As a little callback to the basics, you can listen directly with an anonymous function or hook a function declared earlier.

**Declared:**
```lua
local function onTouch(otherPart)
    print("Part that touched this one:", otherPart)
end

thisPart.Touched:Connect(onTouch)
```

**Anonymous:**
```lua
thisPart.Touched:Connect(function (otherPart)
    print("Part that touched this one:", otherPart)
end)
```

Wait - other clients see my actions!
=

Which is the point of this thread! Understand this: the connection you establish using the above code *is still local*. With the way Touched works however, that means that the client is actively monitoring any part touches. It's not that there's any replication going on here: the client sees that a part touched something and so the signal is fired.

In order to prevent other clients from seeing your actions, you need to verify within the function that the part that touched the object is part of the player's character. This is *only* if you're making local interactions, such as showing shop interfaces like the example a ways above.

To check a part's association with the character, we simply need to run IsDescendantOf. If you consider the parent-child hierarchy for Roblox instances, we can use this to check if the part is part of the character's ancestry.

```lua
local LocalPlayer = game:GetService("Players").LocalPlayer

shopPart.Touched:Connect(function (part)
    -- Let's check that a Character is valid as well
    if LocalPlayer.Character and part:IsDescendantOf(LocalPlayer.Character) then
        print("Our character touched the shop part!")
        shopGui.Enabled = true
    end
end)
```

And just like that, you're set! It's all about verifying that the touched part is part of the LocalPlayer's character, if one exists, then going ahead with the rest of your functions. No remotes, no network traffic, all client-side.

___

That would be all. If you have questions, comments, general feedback, tips for others or add-ons to provide, feel free to post away! I may have missed some things or trailed off where there could be some more detail, so pointing those out would help me and others.

Let's keep all replies constructive and relevant. Happy developing!
