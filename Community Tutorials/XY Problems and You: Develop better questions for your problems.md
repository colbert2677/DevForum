Source: https://devforum.roblox.com/t/xy-problems-and-you-develop-better-questions-for-your-problems/239933

___

I've noticed many XY Problems appearing on Help and Feedback. In light of this, I wanted to create a thread introducing some links related to the XY Problem and talk about it as it relates to the DevForum; what is it, why it's an issue and what we can do to avoid it.

The XY problem does have a [dedicated explanation website](http://xyproblem.info). For quick reference's sake, of course, [XY Problem on Wikipedia](https://en.wikipedia.org/wiki/XY_problem). Both are acceptable sources for learning about the XY problem. I personally find that the former is easier to understand and gain information from.

Understanding the XY Problem and avoiding it is very helpful for when you create threads in the future, whether it's on the DevForum or any other support location. You may have a great question and all, but there may be a better solution or even a broader picture being missed out on.

While the links above are great ways to explain what the XY problem is, I feel a third explanation may be helpful when it's specific to the forums. As a developer who didn't understand this term, let alone know it existed shortly before this tutorial was created, allow me to explain.

___

# What exactly is the XY Problem?

The XY problem refers to asking about an attempted solution, Y over the actual problem, X. This is often because the user doesn't understand the root issue so they attempt to apply a fix which in itself is faulty or the user doesn't know how to do, this spawning a second issue. Problem X is then shelved while the user tries to ask for help repairing solution Y.

# What is the issue with an XY Problem?

The root issue often does not get addressed in an XY scenario. Solution Y either doesn't solve problem X, is a poor resolution or just serves as a band-aid fix. Band-aid fixes should not be relied upon as they are temporary and do not resolve the underlying root issue.

# What is an example of an XY Problem?

I will be using a recent example of an XY problem that I've encountered here. I feel this would be a great example to use since it's also easy to break down and address.

> **X (root problem)**\
> Place1 is experiencing input lag. Controls are not responsive.
> 
> **Y (attempted solution)**\
> Send the player to subsidiary games depending on their device type.
> 
> **Secondary problems**
> - Developer is not sure how to fetch the device that a player is using.
> - Input lag isn't actually addressed.

As you can see from the above, the developer is experiencing input lag in their game. As opposed to trying to diagnose the source of input lag, they resolve to teleport a player to different games based on their type of device and shelve input lag.

There are many reasons why leaving input lag unaddressed and hopping over to teleporting users around is a problem. Other than the very obvious fact that input lag can still occur, there is a list of other reasons why this is not a good idea.

<details>
<summary>Interested?</summary>

- **Roblox does not natively support a way to check what device a player is using.** The way developers have done this so far is to check what input devices are enabled on the client as well as what types of input they are passing via UserInputService.

- **You will separate your communities.** The way matchmaking works on Roblox allows for users to play with their friends, no matter what device they're using. If you, a mobile user wants to play with your friend, a computer user, you will not be able to due to differing devices. That is assuming this teleport system is actually implemented.

- **Maintenance will become significantly difficult for you.** Suppose you have a game that spans across several places. In order to properly implement this system, you now need to make different versions of all of these places: computer, mobile and possibly Xbox. Your place count is now inflated against the formula `n2` (`n3` with Xbox) where `n` is the number of places. So if you have a 10-place game, get ready to maintain 20-30 places.

</details>

# How can the XY Problem be avoided?

Using the example above, the question could've been left at "my game is experiencing input lag". This question would serve as your base. From here, you can either ask some questions such as how to explore performance issues, post code that may potentially be causing client-side lag or do some other self-investigation into the problem.

Most likely, input lag has to do with performance or actual code - that's assuming it only happens in that one place and nowhere else. There are many debugger tools available to you as a developer on Roblox Studio - three good starting places are the [F9 Developer Console](https://developer.roblox.com/articles/Developer-Console), the [Script Performance](https://developer.roblox.com/articles/Improving-Performance) window (this article includes a general article on performance) and the [MicroProfiler](https://developer.roblox.com/articles/MicroProfiler).

For other matters, even including programming, there are lots of forums beyond the DevForum. For example: if you do modelling there is the Blender Forums (if you use Blender) and surely a lot of content you can find with a Google Search about how to do something.

For best results in receiving help about an issue, try applying these practices:

- Include as much information as you can from the getgo. Others require a starting point to work off of to help in investigating or solving your root issue. Less questions are asked to dig information out of you and more time is spent towards providing potential solutions.

- Before responding about an attempted solution not working, make sure to fiddle around with it a bit. If still that doesn't work, feel free to create a response with information about your test. Don't just say a solution hasn't worked for you; explain how it doesn't work and get some console screenshots if you can.

- Explain what solutions you've already attempted and how successful they've been. One of the solutions may actually be the key to tackling the problem but you may just be confused as to how to properly implement it.

- *Always* try doing things yourself first before posting a thread, or test before replying about something. You can often get an answer quicker than waiting hours for responses. If your own attempts aren't fairing well, feel free to create a help thread but also be sure to try tinkering with your problem while waiting for responses. You can depend on us as the DevForum is a learning and helping environment, but don't be too dependent!

I hope this has been of some use to you. There's a lot of reading here, I understand, but I would write it out again if it meant I could provide something for the community to learn from. :slight_smile: 
