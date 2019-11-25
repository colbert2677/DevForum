Source: https://devforum.roblox.com/t/changing-chat-type-and-other-chat-settings-without-forking/313614

___

A popular conversation brought up on the Developer Forum is regarding the modification of the Lua Chat System. Furthermore, within that topic, developers often find themselves wanting to change the chat style between Classic, Bubble and Both. This is due to an update that removed that option from the game settings page in hopes of a better way to configure chat properties in the future.

A common solution I've seen being provided to developers is to fork the chat system's contents and modify the booleans ClassicChatEnabled and BubbleChatEnabled in the ChatSettings module. I don't like this solution for two reasons.

1. You should not be forking the ***entire*** Lua Chat System just to modify two settings. It is possible to change chat types by only forking the ClientChatModules folder and only including ChatSettings in it. This forks that module alone and the rest are inserted as necessary.

2. You should not be forking systems for minor edits. Forking prevents updates to a system and thus you are held responsible for manually updating anything changed. If you don't fork, you get the code inserted directly from the latest CoreScripts branch, which means automatic updates.

With this in mind, I'd like to share with you [Chat.RegisterChatCallback](https://developer.roblox.com/en-us/api-reference/function/Chat/RegisterChatCallback). While there is documentation that briefly explains what you can do with the function and what it's used for, I often feel that it's not explained fully. For this thread, I will be explicitly explaining the option OnCreatingChatWindow. A code examples thread for RegisterChatCallback as a whole is for another time.

Let's grab the documentation for RegisterChatCallback and the OnCreatingChatWindow section.

> RegisterChatCallback binds a function to some chat system event in order to affect the behavior of the Lua chat system. The first argument determines the event (using the  `ChatCallbackType`  enum) to which the second argument, the function, shall be bound. The default Lua chat system uses  `InvokeChatCallback`  to invoke registered functions. Attempting to register a server- or client- only callback on a peer that isn’t a server or client respectively will raise an error. The following sections describe in what ways registered functions will be used.

> **OnCreatingChatWindow**
> 
> Client-only. Invoked before the client constructs the chat window. Must return a table of settings to be merged into the information returned by the ChatSettings module.

The documentation is self explanatory and sufficient here. RegisterChatCallback binds a function to a specific ChatCallbackType and the chat system used InvokeChatCallback to run your functions when specific conditions are met. The condition is typically the ChatCallbackType Enum which summarises very well what something is. I shouldn't have to explain what OnCreatingChatWindow means.

Now, the thing about OnCreatingChatWindow is that it is able to modify the ChatSettings. How can we use this to our advantage and change the chat type? We simply bind a function that returns a table of settings to be modified.

Let's change our game's chat type to Bubble Chat for our example. In a LocalScript preferably under ReplicatedFirst, set this up:

```lua
local Chat = game:GetService("Chat")

Chat:RegisterChatCallback(Enum.ChatCallbackType.OnCreatingChatWindow, function()
    return {
        ClassicChatEnabled = false,
        BubbleChatEnabled = true,
    }
end)
```

Keep in mind that OnCreatingChatWindow can only be used on the client. Don't write it in a server script, that'll produce an error.

And that's it. All you need to know. Have fun. All that text just to lead up to this one small piece of code and not even a satisfactory conclusion. Wow!

Before you go though, there is one last thing that may be of interest to you; remember that I said this has the capability to modify the chat settings. This means that you can return any number of key-value pairs to edit the chat system with.

Here is a full list of the possible settings keys you can include in your settings return table. This is mainly if you're looking for a reference or you haven't forked the chat system before and taken a scroll through the contents of ChatSettings.

I've taken the liberty to not waste time and explain self-explanatory labels, for the most part.

___

> **Chat Behaviour**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|WindowDraggable|Determine whether clients can freely move their chat windows.|Boolean|False|
|WindowResizable|Spawns a tab in the bottom-right corner of the chat window, allowing the user to push or pull it to change the size of their chat window.|Boolean|False|
|ShowChannelsBar|A list of non-private chat channels will be shown at the top of the chat window. Further behaviour modifications available.|Boolean|False|
|GamepadNavigationEnabled|This allows for navigation of the chat window with game pads. A strong doubt you'd ever need it, but someone may.|Boolean|False|
|AllowMeCommand|Enable the dreaded /me [text] command for players to use. Added due to abuse by bad actors.|Boolean|False|
|ShowUserOwnFilteredMessage|Determines if users see their own messages as filtered or not. Still appear filtered to other users. You should probably just leave this alone.|Boolean|True|
|ChatOnWithTopBarOff|If you ever use SetCore("TopbarEnabled", false) but want the chat to still work, this is for you.|Boolean|False|
|ScreenGuiDisplayOrder|Modifies the order of display for the ScreenGui. You probably won't need to touch this.|Number|6|
|ShowFriendJoinNotification|Will send a message to your window if a friend joins your game.|Boolean|True|
|BubbleChatEnabled|The one you probably wanted to see. Self explanatory.|Boolean|IND|
|ClassicChatEnabled|Same as above.|Boolean|IND|

> **Text Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|ChatWindowTextSize|Size of chats in the chat area.|Number|18|
|ChatChannelsTabTextSize|Size of the channel labels.|Number|18|
|ChatBarTextSize|Size of the text you type in the bar.|Number|18|
|ChatWindowTextSizePhone|ChatWindowTextSize for mobile.|Number|14|
|ChatChannelsTabTextSizePhone|ChatChannelsTabTextSize for mobile.|Number|18|
|ChatBarTextSizePhone|ChatBarTextSize for mobile.|Number|14|

> **Font Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|DefaultFont|Universal font.|Enum.Font|SourceSansBold|
|ChatBarFont|Font for the chat bar.|Enum.Font|SourceSansBold|

> **Color Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|BackGroundColor|Chat window background.|Color3|new(0, 0, 0)|
|DefaultMessageColor|Default message colour if ExtraData not set.|Color3|new(1, 1, 1)|
|DefaultNameColor|Default name colour if ExtraData not set.|Color3|new(1, 1, 1)|
|ChatBarBackGroundColor|Background surrounding chat bar.|Color3|new(0, 0, 0)
|ChatBarBoxColor|Actual chat box.|Color3|new(1, 1, 1)|
|ChatBarTextColor|Text inputted into the chat bar.|Color3|new(0, 0, 0)|
|ChannelsTabUnselectedColor|Unselected channels. Use if ShowChannelsBar is on.|Color3|new(0, 0, 0)|
|ChannelsTabSelectedColor|Same as above, except for a selected channel.|Color3|fromRGB(30, 30, 30)
|DefaultChannelNameColor|Self explanatory.|Color3|fromRGB(35, 76, 142)
|WhisperChannelNameColor|Channel when a whisper is open.|Color3|fromRGB(102, 14, 102)|
|ErrorMessageTextColor|Errors sent in the chat area.|Color3|fromRGB(245, 50, 50)|

> **Window Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|MinimumWindowSize| |UDim2|{0.3, 0}, {0.25, 0}|
|MaximumWindowSize| |UDim2|{1, 0}, {1, 0}|
|DefaultWindowPosition| |UDim2|{0, 0}, {0, 0}|
|extraOffset|Calculation to fit chat bar.|Number|(7 * 2) + (5 * 2) or 24|
|DefaultWindowSizePhone| |UDim2|{0.5, 0}, {0.5, extraOffset}|
|DefaultWindowSizeTablet| |UDim2|{0.4, 0}, {0.3, extraOffset}|
|DefaultWindowSizeDesktop| |UDim2|{0.3, 0}, {0.25, extraOffset}

> **Fading Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|ChatWindowBackgroundFadeOutTime|Time until background fades.|Number|0.5|
|ChatWindowTextFadeOutTime|Time before window fades if no interaction with the chat window is made.|Number|30|
|ChatDefaultFadeDuration|How long fades last.|Number|0.8|
|ChatShouldFadeInFromNewInformation|Show chat if new information is sent.|Boolean|False|
|ChatAnimationFPS|?|Number|20.0|

> **Channel Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|GeneralChannelName|Main chat room. Set to nil to prevent chats from other channels showing here (whispers, team chat, so on).|String or nil|All|
|EchoMessagesInGeneralChannel|Messages from other channels show up in main channel. Set to false if using ShowChannelsBar to keep chats to their respective rooms. Main will only show chats from users not in a channel.|Boolean|True|
|ChannelsBarFullTabSize|Number of channels that can be fit into the bar before scrolling enables.|Number|4|
|MaxChannelNameLength|Maximum characters a channel name can have.|Number|12|
|RightClickToLeaveChannelEnabled|Use with ShowChannelsBar as true. Self explanatory.|Boolean|False|
|MessageHistoryLengthPerChannel|How many messages are shown before old chats are deleted.|Number|50|
|ShowJoinAndLeaveHelpText|If help text for joining and leaving channels should be shown. Useful only for custom channels.|Boolean|False|

> **Message Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|MaximumMessageLength|Maximum characters in a chat line. Probably should leave this alone.|Number|200|
|DisallowedWhiteSpace|Prevent this type of whitespace from being entered into chats.|Table|n, r, t, v, f|
|ClickOnPlayerNameToWhisper|Clicking on a name enters a whisper channel with the other player.|Boolean|True|
|ClickOnChannelNameToSetMainChannel|Click a channel to change to it.|Boolean|True|
|BubbleChatMessageTypes|Internal configuration for bubble chats.|Table|N/A|

> **Other Settings**

|Key|Summary|Value type|Default value|
|--|--|--|--|
|WhisperCommandAutoCompletePlayerNames|Typing /w [partialName] autocompletes and enters a whisper with that user.|Boolean|True|

___

Let me know if you have questions, comments, concerns or any other type of feedback. Let's keep it constructive and relevant. Happy developing!
