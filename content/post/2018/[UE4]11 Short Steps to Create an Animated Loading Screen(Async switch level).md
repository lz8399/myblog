+++
title= "[UE4]11 Short Steps to Create an Animated Loading Screen(Async switch level)"
date= "2018-12-20T17:03:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Loading Screen", "Animated"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-007.jpg"
+++

I Went into Window > Levels
<!--more-->

keywords: UE4, Stream Level, Loading Screen, Async Open Level, Async Change Level

11 Short Steps to Create an Animated Loading Screen

1. - I Went into Window > Levels
2. - Created a New Level by going to “Levels” and selecting “Create new Level”
3. - Moved all my main level stuff by highlighting it all in the editor window and selecting “Move Selected Actors to Level” via the “Levels” tab.
4. - Created my load screen texture, camera and animated spinning icon and made sure they were in “Persistent Level”.
5. - In the “Level Blueprint” (Of “Persistent Level”), I created a “Begin Play” event and created a “Open Stream Level” node and connected them both together.
6. - I put the Level Name that I want loaded into the “Open Stream Level” and made sure “Block on Load” wasn’t ticked but “Make visible after load” was.
7. - I created a Matinee with a “Fade” track and an “Event” track. I then made a quick fade in / Fade out / Fade in and put an event while the screen is supposed to be totally black.
8. - I went back into the “Level Blueprint” and created the nodes to “Play” the Matinee once the level has been loaded.
9. - I then added a “MatineeController” node and right-clicked and selected “Refresh nodes” to make my event I created in the Matinee to appear.
10. - I added a node called “Remote Event” which searches all the Level Blueprints for the event in question to fire it.
11. - In the “Level Blueprint” of the level that had just been loaded, I created an event that was called the same thing as the “Remote Event” and connected a “Get Player Controller > Set View Target with Blend” node to it.

And that was all I had to do!

See? 11 short steps to have a fully animated load screen. How awesome is that?!

Reference: Animated Loading Screen  
https://wiki.unrealengine.com/Animated_Loading_Screen

Blueprint Manual Level Streaming  
https://wiki.unrealengine.com/Blueprint_Manual_Level_Streaming

***
`笳鼓动，渔阳弄，思悲翁，不请长缨，系取天骄种。剑吼西风。` ----贺铸·《六州歌头·节选》