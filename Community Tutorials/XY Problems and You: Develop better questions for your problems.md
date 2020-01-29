Source: https://devforum.roblox.com/t/xy-problems-and-you-developing-better-concise-questions-about-your-problems/239933

___

I've noticed many XY Problems appearing on Development Support. In addition to the appearance of these XY problems, I've noticed a lot of mentions of such in the past. In light of this, I wanted to take a bit of time to create a thread introducing some links related to the XY Problem and talk about it a bit. Here is a full run-down - what it is, what you should do and what's wrong with it.

This is an information and resource thread if you're looking for material on the XY problem. More commonly however, the website dedicated to describing the XY problem (below as Link 1) is linked in threads. Feel free to read on!

Link 1: [xyproblem.info](http://xyproblem.info)
Link 2: [Wikipedia](https://en.wikipedia.org/wiki/XY_problem)

Understanding the XY Problem and avoiding it could be very helpful for when you create threads in the future, whether it's on the DevForum or any other support location. You may have a great question and all, but there may be a better solution or even a broader picture being missed out on.

For those of you who are looking for a quick read without opening any of the links, I can try explaining the XY Problem in the best terms I can do.

___

# What exactly is the XY Problem?

The XY Problem pertains to asking about an attempted solution (Y) over an actual problem (X). A secondary issue is spawned due to the application of solution Y in which the user believes will solve the problem X. This leads to the direct problem X being skimmed over to try and repair solution attempt Y.

# What is the issue in an XY Problem?

Often at times, solution Y either does not solve problem X or it is a poor resolution. You could see solution Y as a band-aid fix for problem X, but this means that the root problem still exists.

# What is an example of an XY Problem?

I'd like to use a recent example that came across the forums. I absolutely do not intend to defame the developer who posted this, note that, but I feel like it's an excellent learning point to reference from.

*Problem X (Root Problem):* Place1 is currently experiencing input lag.
*Attempted Solution Y:* Players are teleported to subsidiary (side) games based on their device type.
*Secondary Problem:* Unsure of how to fetch the device that a player is using.
*Leftover Problem:* Input lag is left unaddressed in order to try fixing or applying Y.

# How can the XY Problem be avoided?

Using the example above, the question could've been left at "my game is experiencing input lag". This question would serve as your base. From here, you can either ask some questions such as how to explore performance issues, post code that may potentially be causing client-side lag or do some other self-investigation into the problem.

Most likely, input lag has to do with performance or actual code - that's assuming it only happens in that one place and nowhere else. There are many debugger tools available to you as a developer on Roblox Studio - three good starting places are the [F9 Developer Console](https://developer.roblox.com/articles/Developer-Console), the [Script Performance](https://developer.roblox.com/articles/Improving-Performance) window (this article includes a general article on performance) and the [MicroProfiler](https://developer.roblox.com/articles/MicroProfiler).

Without getting too much into the example ordeal, the linked resources explain the XY Problem and avoiding it better. Just like Scripting Support guidelines, you should always be sure to:

- Include as much information as you can. Others require a starting point to work off of to help in investigating or solving your root issue.
- Provide as much detail as you can when others ask for more information. This helps looking into the issue a little less of a chore.
- Explain what solutions you've already attempted and how successful they've been. One of the solutions may actually be the key to tackling the problem.
