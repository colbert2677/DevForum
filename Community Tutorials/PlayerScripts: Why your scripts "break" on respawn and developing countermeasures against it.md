Source:

___

PlayerScripts is a client-side container that mirrors ServerScriptService. Whereas ServerScriptService is designed for server-side code (Scripts and ModuleScripts only required by Scripts), PlayerScripts is designed for client-side code (LocalScripts and ModuleScripts only required by LocalScripts). The client does not have access to ServerScriptService's contents and the server cannot access PlayerScripts. It is populated by the contents of StarterPlayerScripts upon creation.

Long before PlayerScripts existed, the best way to include any client-side code independent of a ScreenGui was to directly place LocalScripts in Backpack or PlayerGui, or create a Model that contained LocalScripts for the game in either of these folders. PlayerScripts now have effectively superseded this practice and have made the creation of client-side systems much easier to deal with natively.

There's just one exception. Accounting for respawns.

It's not uncommon to come across a help thread in Scripting Support where a developer is having trouble with a script placed in StarterPlayerScripts where they'll mention that their code stops working after the character respawns. In light of this, I'd like to take a bit of time to explain what the issue is and what we can do to combat it.

___
