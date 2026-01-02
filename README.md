# Chocobo GP Documentation (wip)
Documentation of CGP's internal filestructure and what stuff does in the context of the game

**NOTE:** No actual game code is found here, just parameter files and references to the game code. Whenever I say something has "code" in it, I actually mean that it points the game to where its code is in the executable, it's not something we can modify yet.
Unless it's blueprint code.
Stuff marked with (wip) is not fully understood. Stuff marked with (x) is either obfuscated/blueprint code or is irrelevant for modding as far as I understand it.

# `BasicMaterials` (wip, prolly unused)
As the name suggests, the folder contains some very basic materials for colors, normal maps, and whatever `T_basic_orm` stands for

# `Camera` (wip)
Parameter files for the camera to tell it what to do in specific contexts (e.g. screenshake for quake)

# `Course`
Folder containing **data** (not assets) for the game's tracks
## `Data`
Subfolder containing the 26* tracks's data files. For information on these files' data structure, check [this](https://github.com/Nintbros/ChocoboGP-Documentation/blob/main/TrackDataStructure.md).

*Story mode technically uses its own tracks, making the total be technically higher, but those aren't here.
## `Meshes` (wip, probably unused)
Road and dirt textures, resembling Cid's Test Track's. No clue what this is doing here, track models are elsewhere. Might be a remnant from development.

## `RouteMaps`
Folder containing all the Minimap textures.

## `Story_Data`
Folder containing the track data for Story Mode.

For some reason, Story Mode uses entirely unique tracks, completely independent from the regular tracks in the main game, except for the fact they use the same models*.

This is why BBH in the prologue is barren and has no items*.

Fun fact! Story mode doesnt use a custom itemset like how you can do in online, it bakes the available magicite to be pulled into the track data itself, essentially "hardcoding" it. Pretty neat!


*BBH is an exception in that it has its own separate level file which is a carbon copy of the regular track, minus the fact it has the boost pads and conveyers removed. Boost pads & trick ramps have their hitboxes dictated by the track data files, but their visual models, as well as course gimmicks (such as conveyers) are dictated in the level file. BBH is the only exception and every other story mode race loads the same exact level as the proper tracks you can race online in.
## `System` (x)
Folder containing the Course Manager BP and some unused stock placeholder files. It also contains a datatable dictating the default full item set which is odd because every track dictates this individually. Maybe it was for copy pasting. Or maybe it is unused on the track's side, I dunno. I don't have UE4SS to disect the game with.

# `Effect`

This is where particle effect data for every character is stored. Such as the particle animations used for their ults, where the exhaust pipes are so the miniturbo flames can appear properly, and stuff like that.

# `GameMain` (x)

This is what loads when you first boot the game. It loads the rest of the game and then kind of just exists. Based off of the names, anyway.

# `Gameplay` (x)

Folder containing the Game Manager BP and the Mirror Mode screen material. Sure.

# `Item` (x)

Folder containing the Item Box Manager BP, Item Box and Crystal BP, and the list of Item IDs in the game.
Like. For the shop, for example. Not for item boxes in races.

Thank you, Square Enix. Awesome file organization.

# `L10N`

Standard UE folder. Contains localised strings for every language.

# `Localization`

Standard UE folder. Contains the localisation files.

# `NPC`

Folder containing the models, textures, BP code and animations for this game's Lakitu equivalent (does he even have a name?) and Shirma's Kurukuru. Specifically just those two. They're IDs 01 and 04 respectively, and no other NPCs are in here, so draw your own conclusions.

# `Player`

This one is understandably big, so, let's go folder by folder.

## `abilities`

Judging by the names (`GA_Back`, `GA_Drift`, `GA_Goal`) these are probably the blueprint files for the core game actions. Presumably `GA` stands for "Game Action". There's also "Game Effect" (`GE_DriftDash`, `GE_StartDash`, and `GE_WheelSpin`).

This folder also has several subfolders containing every character's ult BP code, some magicite BP code, more Game Actions relating to damage or spinning out, global ult debuffs, and some miscellaneus BPs like i-frames I'm guessing.

## `param`

Big folder containing a lot of datatables. Like a lot of em.

Includes datatables such as: 

>Unused stuff

>The weekly and daily quests you got given out back when the game was alive

>CPU difficulty

>Some params for some magicite

>The player datatable

>Stat set for Beginner speed and Master speed

>Whatever the fuck `DT_PlayerRankSpeed` is

>Sticker datatable

>And 3 datatables for each character's skins (so for example, Volg has 6 datatables, 1 for default skin on neutral ride, default on grip ride, default on speed, crystal on neutral, etc.) establishing some properties about them (like their color variations and where stickers go)

## `plXX`

One folder for each of the game's 34 racers, + pl00 (template + some common stuff) and pl99 (bahamut).

Save for those 2, they each contain the BP file for that character (dictating stuff like their hitbox size and what model they load), and of course the models and animations for each characters' skins.


# `Race`

Folder containing Manager BPs for all the main modes of the game (GP, offline GP, TTs, Story Mode, etc) as well as some datatables, such as the amount of points gained in private lobbies for each placement, amount of GP Points gained from online matchmaking results, offline Grand Prix cups and their associated CPU difficulty levels, Story Mode race parameters (such as the CPUs that may appear and what vehicle and difficulty they use), and most importantly the Track Select datatable. Pretty important for [adding tracks to Track Select!](https://github.com/Nintbros/ChocoboGP-Documentation/blob/main/AddTrackToTrackSelect.md)

# `Replay`(x)

This folder houses all 52 staff ghosts! They're just chillin' in there :)

They use the same format as personal ghosts, so you can drop your own Time Attack ghost files from your save data in here, rename accordingly, and make your own Staff Ghosts for, for example, custom tracks. Pretty neat!

The format for the ghost files themselves isn't understood though and I am sure as hell not reverse engineering them.

# `Scene` (x)

General BP code files for handling all the different scenes of the game It's only menus, though.

# `Sequence`

Contains the camera intro cutscenes for every course in the game, including the 4 unused tracks! Also contains a datatable naming all of these for some reason. No clue why they would do that, intro sequences are pulled from the track data files. The unused tracks are referred to as "demos" within said datatable, so. It also dictates which story mode chapter it belongs to, since apparently at the bottom it also includes all the camera sequences used in story mode.

# `Shell` (wip)

Basically all of the Ult and Item code is found here

# `Shop` (x)

This folder contains `shop.dat`. I have no clue what the fuck it is. It scares me.

# `Sound` (wip)

This folder contains all the sound stuff and whatever
Truth be told I've yet to look at it lol

# `Stage` (wip)

Another huge folder housing all of the 3d assets and textures for every track in the game, as well as an unused, dummy track, and what appears to be leftovers of a test track

# `Story` (wip)

Folder containing all the assets for Story Mode's cutscenes

# `StringTable`

This behemoth of a file exists to tell the game which message IDs correspond to what strings of text

# `Test` (wip, unused)

Boy I sure do love me some unused content!

# `UI` (wip)

Folder i havent really looked at that houses a buncha stuff for the UI in general (menus, game and system)

# `Watermark`

<img width="245" height="47" alt="imagen" src="https://github.com/user-attachments/assets/c63995bf-041d-4df5-bd9c-4c7de44dd420" />

I hate you
