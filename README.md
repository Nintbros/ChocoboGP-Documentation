# Chocobo GP Documentation (wip)
Documentation of CGP's internal filestructure

**NOTE:** No actual game code is found here, just parameter files and references to the game code. Whenever I say something has "code" in it, I actually mean that it points the game to where its code is in the executable, it's not something we can modify yet.
Stuff marked with (wip) is not fully understood. Stuff marked with (x) either needs to be reverse engineered or is so obfuscated there's no point in trying to understand it.

# `BasicMaterials` (wip, prolly unused)
As the name suggests, the folder contains basic materials that seem unreferenced by the game

# `Camera` (wip)
Parameter files for the camera 

# `Course`
Folder containing **data** (not assets) for the game's tracks
## `Data`
Subfolder containing the 26 tracks's data files
## `Meshes` (wip, probably unused)
Road and dirt textures? No clue what this is doing here, track models are elsewhere. Might be a remnant from development.

## `RouteMaps`
Folder containing all the Minimap textures

## `Story_Data`
Folder containing the track data for Story Mode.

For some reason, Story Mode uses entirely unique tracks, completely independent from the regular tracks in the main game, except for the fact they use the same models.

This is why BBH in the prologue is barren and has no items.

## `System` (x)
Folder containing the Course Manager and some unused files

# `Effect` (wip)

Probably some VFX settings (like for example where should miniturbo spark particles come from)

# `GameMain` (x)

This is what loads when you first boot the game. It loads the rest of the game and then kind of just exists.

# `Gameplay` (x)

Folder containing the Game Manager

# `Item` (x)

Folder containing the Item Box Manager, Item Box and Crystal data/code (i still cant tell), and... the list of Item IDs in the game.
Like. For the shop.

go home squeenix youre drunk

# `L10N`

Folder containing localized UI assets (e.g. the "action text" that pops up on the left of the screen when you do something)

# `Localization`

General localisation files, it's where all of the game's text is stored

# `NPC`

Folder containing the models, textures, code and animations for "Lakitu" and Kurukuru

# `Player`

will finish some other day because this folder is HUGE

basically it contains player code, player stats, ult params, magicite code?, and player models and whatnot

# `Race`

Folder containing Managers for all the main modes of the game (GP, offline GP, TTs, Story Mode, etc) as well as some menu data for each track select (for example, which button loads what track)

# `Replay`(x)

This folder houses all 52 staff ghosts! They're just chillin' in there :)

# `Scene` (x)

General code stuff for handling all the different scenes (menus/gameplay) of the game

# `Sequence` (wip)

A folder containing a Sequence manager and a bunch of demo files for all the tracks in the game, no clue what these are, though they might be camera intro sequences

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
