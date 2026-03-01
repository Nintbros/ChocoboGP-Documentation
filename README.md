# Chocobo GP Documentation (wip)
Documentation of CGP's internal filestructure and what stuff does in the context of the game

**NOTE:** No actual game code is found here, this is documentation for the internal filestructure for modding purposes. When I refer to something as "code" I mean Blueprint (BP) code.
The game's executable is wholly off-limits, due to being a Nintendo Switch game. If you want to be the madlad to reverse engineer it, be my guest.
Stuff marked with (wip) is not fully understood. Stuff marked with (x) is either obfuscated, blueprint code we should not be touching, or is irrelevant for modding as far as I understand it.

# `BasicMaterials` (unused)
This folder contains some dummy materials that go entirely unused.

# `Camera` (wip)
Camera effect and movement files. Contains files for Quake/Quakera/Quakega's screenshake, as well as the race results camera.

# `Course`
Folder containing **data** (not assets) for the game's tracks
## `Data`
Subfolder containing the 26* tracks's data files. For information on these files' data structure, check [this](https://github.com/Nintbros/ChocoboGP-Documentation/blob/main/TrackDataStructure.md).

*Story mode technically uses its own tracks, making the total be technically higher, but those aren't here.
## `Meshes` (unused)
Unused, remnant from development. Contains early assets for Cid's Test Track.

## `RouteMaps`
Folder containing all the Minimap textures.

## `Story_Data`
Folder containing the track data for Story Mode.

For some reason, Story Mode uses entirely unique tracks, completely independent from the regular tracks in the main game, except for the fact they use the same models*.

This is why BBH in the prologue is barren and has no items*.

Fun fact! Story mode doesn't use a custom itemset like how you can do in online, it bakes the available magicite to be pulled into the track data itself, essentially "hardcoding" it. Pretty neat!


*BBH is an exception in that it has its own separate level file which is a carbon copy of the regular track, minus the fact it has the boost pads and conveyers removed. Boost pads & trick ramps have their hitboxes dictated by the track data files, but their visual models, as well as course gimmicks (such as conveyers) are dictated in the level file. BBH is the only exception and every other story mode race loads the same exact level as the proper tracks you can race online in.
## `System` (x)
Folder containing the Course Manager BP and some unused stock placeholder files. It also contains a datatable dictating the default full item set which is odd because every track dictates this individually. Maybe it was for copy pasting. Or maybe it is unused on the track's side, I dunno. I don't have UE4SS to disect the game with.

# `Effect`

This is where particle effect data for every character is stored. Such as the particle animations used for their ults, where the exhaust pipes are so the miniturbo flames can appear properly, and stuff like that.

# `GameMain` (x)

This is what loads when you first boot the game. It loads the rest of the game and then kind of just exists. Based off of the names, anyway.

# `Gameplay` (x)

Folder containing the Game Manager BP and the Mirror Mode screen material. Sure.

# `Item`

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

General BP code files for handling all the different scenes of the game. It's only the menus, though.

# `Sequence`

Contains the camera intro cutscenes for every course in the game, including the 4 unused tracks! Also contains a datatable naming all of these for some reason. No clue why they would do that, intro sequences are pulled from the track data files. The unused tracks are referred to as "demos" within said datatable, so. It also dictates which story mode chapter it belongs to, since apparently at the bottom it also includes all the camera sequences used in story mode.

# `Shell` (wip)

Within the context of Chocobo GP, a Shell is a spawnable entity the racers can summon under certain circumstances. For example, Magicite or Ult projectiles. Miscellaneous race entities, like Checkpoints, boost pads and void out triggers also count as Shells internally. This folder contains a bunch of Blueprint code files for some of the Magicite, some of the Ults in the game, and the miscellaneous race entities. It is worth pointing out that /Shell/Abilities contains a file named `A_TestShell`. Pretty neat.

The Magicites without a Shell BP are: Haste, MBarrier, Bahamut.
I am too lazy to go through all 34 Ults but, eyeballed, only half of them have BP files here.

This folder also contains a DataTable with some parameters for some of the Shells, and it actually seems to change things. So that's cool.

# `Shop` (x)

This folder contains `shopitems.dat`. It is a binary file that somehow determines the items listed in the shop. It scares me.

# `Sound` 

This is another big set of folders, so strap in.

In this main folder are contained the SoundManagerBP, as well as `U_VoiceDataSetting`, which dictates which PLID (Player ID) uses what set of voicelines.

Further, it contains two datatables, one listing out every BGM in the game, tying them to an item ID, and defining some characteristics about them (e.g. `bUsableAsRaceBgm`), and one listing out every Sound Effect in the game, as well as denoting if it is a system sound effect.

Now, for the subfolders:

## `_Others` (Unused)

<img width="492" height="79" alt="image" src="https://github.com/user-attachments/assets/d57cd25c-d5bd-4f2a-9d02-a2a8436d491c" />

Say hello to `SQ_Dummy`. It does absolutely nothing.

## `Attenuation` (x)

I'm gonna be very real. I'm not a sound kind of person. I don't know what Attenuation is supposed to mean in games. But I can tell you that this folder just houses another probably unused sound asset. Or if it is used, we probably should not be touching it anyway.

## `Bgm`

Okay, on to actually relevant things. This here folder contains all 85 music tracks found in Chocobo GP. They are all in Square Enix's proprietary sound format. Luckily, Audiomog works perfectly fine with CGP's sound uassets, so we have full control over them. For more information on BGM replacement, check out [this other readme](https://github.com/Nintbros/ChocoboGP-Documentation/blob/main/AddCustomSongToGame.md).

## `Se`

Folder containing other sub-folders.

### `Game`

This folder contains all 252 race sound effects. Thing's like Ultima's sound effect, online GP matchmaking sounds, Ult SFX, the works. They all use SQEX's proprietary sound format.

This folder also itself houses an `Engine` subfolder, which houses all the looping sound effects for all the racing engines in the game.

### `Stage`

Subfolder containing all stage ambiance and hazards SFX.

### `System`

Subfolder containing generic system sound effects for menuing.

## `VirticalSlice` (unused)

If you are familiar with the concept of Vertical Slices, and adore early content, you might have just smiled. Housed here is a subfolder called `SE` that contains several sound files, including race SFX, system SFX, and even a song or two, used for CGP's January 2020 demo (which is as far as I am aware, lost media). These are for the most part early versions of final SFX and are noticeably different from the final game.

## `Voice`

Contains both the English and Japanese racing voice clips for all 34 characters, organized by PLID.

## `VoiceList`

Same as above, except housing DataTables mapping each voice file to the respective proper voice line response in-game.

# `Stage` (wip)

Another huge folder housing all of the 3d assets and textures for every track in the game, as well as an unused, dummy track, and what appears to be leftovers of a test track

# `Story` (wip)

Folder containing all the assets for Story Mode's cutscenes

# `StringTable`

Standard UE folder. Maps text strings to their entries in the Locres file.

# `Test` (unused)

Boy I sure do love me some unused content!

# `UI` (wip)

Folder i havent really looked at that houses a buncha stuff for the UI in general (menus, game and system)

# `Watermark`

<img width="245" height="47" alt="imagen" src="https://github.com/user-attachments/assets/c63995bf-041d-4df5-bd9c-4c7de44dd420" />

I hate you
