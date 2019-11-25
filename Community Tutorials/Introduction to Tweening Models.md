Source: https://devforum.roblox.com/t/introduction-to-tweening-models/315253

___

One of my personal favourite services on Roblox is the TweenService. Honestly, who doesn't like some smooth transitioning in their interfaces or even just any element of their game? Eye candy is always something to appreciate, unless there's too much of it.

Almost a year ago, I had written a tutorial titled [Brief Introduction to Tweening Models](https://devforum.roblox.com/t/brief-introduction-to-tweening-models/178948). This tutorial was fairly simplistic, rushed and didn't cover the topic as appropriately as it should've. Tweening models seems to be a fairly relevant topic nowadays. There's many ways to do it, but then one of the few or only tutorials dedicated to the topic isn't fleshed out well.

With all this in mind, I present you a new tutorial, **Introduction to Tweening Models**. It is the latest article that provides information for model tweening and is fit to current standards. While this is a detailed thread, I call it an introduction mostly because this describes *a* process to tweening models. It does not cover all possible model tweening methods and serves more as a "here's how to get started and here are some things you should keep in mind".

Apologies in advance for not including a table of contents. Maybe later.

___

Understanding Tweening
=

For the newies here who hopped straight to tweening models rather than learning tweening as a whole, let's define what a tween is really quickly. I'll admit now, these are not all my words.

Tweening is the process of creating intermediate frames between two key frames. This creates a visual effect where you see something essentially glide or evolve from the first key frame to the second.

Tweening on Roblox is no different. When you see a Gui moving smoothly from point to point, that is a tween. When you see a number slowly crawl up, increment quickly and then slow down in counting upwards, that too is in fact a tween.

___

Concept of Tweening Models
=

Something to understand regarding tweening models is that you aren't actually tweening a model. Might sound strange for a tutorial on tweening models, but that's how it is. When talking about model tweening, the discussion is really about moving a model relative to a helper part.

Tweens are restricted to singular objects, especially if you're using TweenService. Custom tween implementations are also singular, though modules that support multiple object tweens create that illusion via pseudothreading (spawn / coroutine) or iterating over a set of items.

___

Rigging Your Model
=

The important part to this tutorial is rigging your model. Somewhere, somehow, you require a root that will serve as the moving part for your assembly, to which all other parts will be attached to. This root can either represent your entire model, or just a hinge. The point is that only this part moves.

One of the more common use cases for model tweening may be moving a door or a casing for something, though there may be many other uses for model tweening that you may come up with.

First off, get your model. For this tutorial, I've constructed a model really quickly off the fly. It's a simple panel. Our simple panel here could be turned into a solid model and we could move it as one part, but we don't do that because we want to keep materials in.

**Our panel:**
![image|521x500,50%](upload://qwxhpqf7c4I3YLGC8IwLf7MV56o.jpeg) 

Setting Up the Root
-

Start by adding a root part to this panel. This is the part we mentioned that will be the only part doing any actual moving and what we will call tweens on.

For a model that will rotate, you will need to make a hinge. This can be done by creating an invisible pole with the same width and depth, as well as the height of your model. The panel will swing around this hinge when you go to tween its rotation.

![image|538x485,50%](upload://velZjo9ihG6g2VKHxZTu2lIXHrC.jpeg) 

For a model that slides around or doesn't need to swing, any kind of root is fine. I personally prefer a root that covers the entire model and forms a bounding box for the sake of being able to move accurately as if I'm moving the model itself, not a proxy.

![image|643x500,50%](upload://xHMw6mxCPQpHyXGz3enr7XXbXF4.jpeg) 

**Make sure that your root is rotated properly.** This can affect the way your CFrame math works. Typically, what I do to confirm the positive directions of the hinge is to write a quick piece of code in my console after *selecting* the hinge. You *must* select the hinge for this to work.

```lua
local Selection = game:GetService("Selection"):Get()[1]

local NormalIds = {
	[Enum.NormalId.Top] = BrickColor.new("Lime green").Color,
	[Enum.NormalId.Front] = BrickColor.new("Really blue").Color,
	[Enum.NormalId.Right] = BrickColor.new("Really red").Color
}

for NormalId, HandleColor in pairs(NormalIds) do
	local Handles = Instance.new("Handles")
	Handles.Color3 = HandleColor
	Handles.Style = Enum.HandlesStyle.Movement
	Handles.Faces = Faces.new(NormalId)
	Handles.Adornee = Selection
	Handles.Parent = Selection
end
```

![image|690x430,50%](upload://hW6ZcmoCuZo8Ydn3IUgr5difL27.jpeg) 

The above code gets arrows for the top, front and right directions, all three of which are typically used to determine positive directions in 3D space given no specification. We use these colours to help determine where our root should be rotated towards.

- The green arrow should never be facing any other direction than the top. If so, rotate and resize the root accordingly so the green arrow points upwards. This is a concrete rule of thumb.
- The red and blue arrows respectively must indicate a front-facing and right-facing direction. It typically doesn't matter where these are placed, so long as your rotation axis is fine.

You can delete them once you've confirmed the directions of your parts are facing the right way.

Attaching the Model
-

Once you've decided on the root and way your model should move, we now must move on to get the model hooked to that root. We must do two things:

- Unanchor the entire model, anchor the root.
  - The unanchoring helps us to move the other parts with the root. The root needs to be anchored to prevent the panel from flying about.
- Weld the model's parts to the root using **WeldConstraints**.
  - WeldConstraints are a superior option to other joints. This will be explained later.
- Optionally, third thing, set the collision of the model to false but the root to true. Only do this if you use a root that covers the whole model and collisions with the actual model aren't important.

To automate this process, I usually use a certain chunk of code that gets the children of the model and welds them to the root. For models that have other parts or models in them, you may want to think about GetDescendants or matching the roots of those models (PrimaryPart) to the root of the main model (tween proxy).

The following code is ran in the command bar. I like my models welded in Studio sessions as opposed to doing so in live servers, plus welding in Studio is necessary to prevent any discrepancies in running servers such as slightly dispositioned parts.

```lua
local Panel = workspace.Panel
-- Using Panel.PrimaryPart for convenience's sake
local Part1 = Panel.PrimaryPart

for _, Part0 in pairs(Panel:GetChildren()) do
	if Part0:IsA("BasePart") and not (Part0 == Part1) then
		local WeldConstraint = Instance.new("WeldConstraint")
		WeldConstraint.Part0 = Part0
		WeldConstraint.Part1 = Part1
		WeldConstraint.Parent = WeldConstraint.Part0
		
		Part0.Anchored = false
	end
end

Part1.Anchored = true
Part1.CanCollide = false
```

After this, we can turn on the constraint viewer to see a visual representation of what welds are doing and if we've got everything. A properly welded model should have everything ultimately leading up to the root and none of the welds should be drawn grey. If a weld appears grey, it's welding two anchored parts and that needs to be corrected.

![image|360x123](upload://1mjpLSSWrMWCAegMDCXBsI8B6yY.png) 

Let's have a look at our welded panels.

![image|690x384,50%](upload://dA2avol2tcvRdAcEcwAKfjcmDAc.jpeg) 

And with this, you have finished rigging your model. There is only one more step after this and it's to apply your tweens to the model. The fun part and what you've probably been waiting for.

___

Tweening Your Model
=

Once your model has been rigged up, you are completely set. There's a reason I called this thread an introduction and that's because all there is to tweening models is attaching your model's BaseParts to a rig and moving that BasePart around. Turns out it's not that difficult to tween models, huh?

For any kind of tweening on the platform, you are strongly encouraged to use the TweenService as tweens are handled for you on the backend and sport a sufficient amount of functionality to get you through. The only time I'd think about a custom implementation is for creating easing styles or expanding the capabilities of the TweenService.

To help you get started, I will provide two code samples available for each respective panel. The first code sample is used to rotate the panel. As far as this goes, you will want to tween the model using CFrame.Angles. **Make sure your inputs are in radians.**

```lua
local TweenService = game:GetService("TweenService")

local Panel = workspace.Panel
local PanelRoot = Panel.PrimaryPart

local PanelSwingInfo = TweenInfo.new() -- Let's use all defaults here

local PanelSwingTween = TweenService:Create(PanelRoot, PanelSwingInfo, {
    CFrame = PanelRoot.CFrame * CFrame.Angles(0, math.rad(180), 0)
})

PanelSwingTween:Play()
```

And here is our result:

https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/b/e/9/be9962b19daa90e5e01e276d322e281104d8d52b.mp4 

As for the second one, we simply need to take the logic of the first one and configure it a little. Let's have the door move by its own size to the right, along with extra offset so it gets the door sliding into a wall feel.

```lua
local TweenService = game:GetService("TweenService")

local Panel = workspace.Panel
local PanelRoot = Panel.PrimaryPart

local PanelSlideInfo = TweenInfo.new() -- Let's use all defaults here

local PanelSlideTween = TweenService:Create(PanelRoot, PanelSlideInfo, {
    CFrame = PanelRoot.CFrame * CFrame.new(PanelRoot.Size.X + 0.1, 0, 0)
})

PanelSlideTween:Play()
```

That code will give us this:

https://doy2mn9upadnk.cloudfront.net/uploads/default/original/4X/5/6/d/56dc3b8079567a625d7556e4477801b0463b7730.mp4 

And with that, you are done. You now understand how to tween models, you are intrigued and you are now inclined to go tween a model. Eventually, you will have model tweens everywhere. Hahaha.

___

Addressing Potential Concerns & Practices
=

Now that the process has been covered, let's look further. There is still quite a bit of information to take in. You can skip it if you aren't interested, or stay and read for the sake of knowledge. Either way, I'd like to take some time to explain some of the thought processes behind my methods as well as other methods and address any potential concerns. I've had a few debates on my practices as well.

A Bad Legacy Method
-

The method I had accepted as a solution to an old thread asking how to tween models was to make a dummy CFrame object, tween that CFrame object and then call SetPrimaryPartCFrame on the model to that value every time it changed. The code for that is as follows:

```lua
local tweenService = game:GetService("TweenService")
local info = TweenInfo.new()

local function tweenModel(model, CF)
	local CFrameValue = Instance.new("CFrameValue")
	CFrameValue.Value = model:GetPrimaryPartCFrame()

	CFrameValue:GetPropertyChangedSignal("Value"):connect(function()
		model:SetPrimaryPartCFrame(CFrameValue.Value)
	end)
	
	local tween = tweenService:Create(CFrameValue, info, {Value = CF})
	tween:Play()
	
	tween.Completed:connect(function()
		CFrameValue:Destroy()
	end)
end
```

Don't use this code. I'm showing it to you so you can see it, but you absolutely better not do that after I took the time to explain a better method of how to tween a model.

Anyway, here are some of the issues raised with this solution:

- The bottleneck is that ValueObject. This whole method relies on it. The moment that ValueObject goes, you have a problem on your hands.
- You cannot use this without explicitly setting a PrimaryPart for the model. SetPrimaryPartCFrame will throw an error asking for a PrimaryPart to be set.
- SetPrimaryPartCFrame itself is terrible. I will explain that in depth below.
- Introduces unnecessary overhead and overcomplication to a simple problem by adding more instances and management processes to your code.

This method is still being passed around and used in some cases. *Please do not accept that as a solution or good answer.* You'll find yourself battling with the code more times than you deserve to be.

Using SetPrimaryPartCFrame
-

If you've noticed, I had not used SetPrimaryPartCFrame anywhere in my code, despite this being the canonical way of addressing a model's CFrame. In fact, using this function was one of the earliest proposals of how to tween a model. I hate this method entirely.

The problem with SetPrimaryPartCFrame is that because of the way the backend handles offset calculations from the PrimaryPart, it is capable of producing floating point errors easily. This results in your model being torn apart. The rate at which this happens is very slow, but given time and many calls, the tearing and seams in your models become visible. This is a common complaint about the use of the function and thus developers tend to stay away from it.

For those of you curious about the debacle on SetPrimaryPartCFrame, you can search up the function itself and you'll see a lot of complaints about using the method. Here's a thread I recommend, as it has responses from experienced developers and a former engineer:

https://devforum.roblox.com/t/setprimarypartcframe-gradually-offsets-component-parts/16041

A way to fix this issue is to handle SetPrimaryPartCFrame yourself with a custom full-Lua implementation. In this implementation, you cache the CFrames of every part except the root in a dictionary and manually offset them from the PrimaryPart when it moves. This is done by multiplying the inverse of all the part CFrames by the PrimaryPart's CFrame. This keeps all model parts in relative space to the PrimaryPart.

```lua
local offset = primaryPart.CFrame:ToObjectSpace(boundPart)
primaryPart.CFrame = primaryPart.CFrame * CFrame.new(1, 2, 3)
boundPart.CFrame = primaryPart.CFrame:ToWorldSpace(offset)

-- You can also use CFrame inverse, which is what ToObjectSpace is internally

primaryPart.CFrame = primaryPart.CFrame * CFrame.new(1, 2, 3)
boundPart.CFrame = primaryPart.CFrame:Inverse() * boundPart.CFrame
```

This solution goes for those who want to anchor all the parts of their model and skip out on using a root PrimaryPart exclusively. That being said, you can still make the root of your model a visible part rather than a proxy part.

I'm not a very huge fan of this solution. I'm not a math-centric person and prefer something quick and easy to work with. As well, the user that suggested this solution to me ended up following the same paradigm as the first one with the proxy value.

Orientation of the Root Part
-

Something I stressed earlier in the tutorial under the section **Setting Up the Root** was that the orientation of it must be in appropriate positive coordinates. I provided both a code sample and an image to help this become more apparent.

Remember that the tweening is performed on the root. If the orientation of the root is not appropriate according to the way the model is constructed, this can cause you a bit of trouble trying to figure out which axis is the current one to turn. For example, if your top direction is facing right instead.

Always check your root's orientation before proceeding with the rest of the tutorial. Once you make a mistake, it's time consuming and annoying to go back over those errors and correct them.

Attaching Parts
-

This tutorial mainly states that the method we're going to use is welding unanchored parts to an anchored root, which we tween. As you can see from the videos, this works excellently.

In order to make the parts dynamic and move relative to the root without actually performing any math operations on them, we unanchor the parts and attach them to the root with welds. This gives us the ability to control one part and by nature, control the rest.

A huge bone that was picked in this method is that it uses unanchored parts. The argument raised was that the unanchored parts were causing undue physics simulation. For a while, I didn't have any counterexplanation and dodged answering the question until I did some investigations myself; this statement is false. And the falsity of this statement makes this method more powerful.

Unanchored parts indeed do get physically simulated, however any part welded to another is not actually physically simulated. In this scenario, the unanchored parts welded to our root are static and do not cause said undue physics simulation. The rest of the model behaves like its anchored.

You therefore don't have to worry about any physics throttling or unintended physics issues while using this method. It is safe to your performance. :slightly_smiling_face:

WeldConstraints
-

Within this tutorial, I had mentioned that WeldConstraints are a superior option to other joint instances. I mean this very literally and the same goes for the rest of the constraints system. If you haven't already been introduced to WeldConstraints or haven't started using them, please do. WeldConstraints are absolutely lovely.

I have been asked in the past is if there's any difference to using WeldConstraints and other joint instances. Application wise no but workflow wise yes. WeldConstraints have the absolute luxury of not needing to set C0/C1 - any part you connect with a WeldConstraint is welded relative in rotation and position to each other and this is done automatically.

Here is a code sample comparison when using WeldConstraints and not.

```lua
local Weld = Instance.new("Weld")
Weld.Part0 = RootPart
Weld.Part1 = ModelPart
local Offset = CFrame.new(ModelPart.Position)
Weld.C0 = RootPart.CFrame:Inverse() * Offset
Weld.C1 = ModelPart.CFrame:Inverse() * Offset
Weld.Parent = Weld.Part0

local WeldConstraint = Instance.new("WeldConstraint")
WeldConstraint.Part0 = ModelPart
WeldConstraint.Part1 = RootPart
WeldConstraint.Parent = WeldConstraint.Part0
```

Of course, using one or the other is completely up to you, but I would highly recommend WeldConstraints. I've switched most of my weld work over to WeldConstraint in circumstances where I need another joint type. Specifically, Motor6D, for the sake of animations.

___

Constraints in General
-

Did you know? You don't have to follow this tutorial down to the skeleton to be able to move models. You can actually use the constraints system collectively to create moving assemblies. You just have to follow the same rigging process and then it's completely up to you where to go from there.

That's a follow-up tutorial for another time. :wink:

___

That's all for now! Thanks for dropping by. If you have any questions, comments, concerns or other feedback to share, feel free. Let's keep it all constructive and relevant. Happy developing!
