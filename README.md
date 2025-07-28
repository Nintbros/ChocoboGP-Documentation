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
# Track Data File Structure
## `Level`
This property dictates which track model & collision gets loaded
<img width="750" height="31" alt="imagen" src="https://github.com/user-attachments/assets/9439f4e5-4398-46e2-b58a-2ada3e3e3565" />
## `IntroductionDemo`
This tells the game which camera sequence file to pair alongside the track
<img width="656" height="25" alt="imagen" src="https://github.com/user-attachments/assets/97f8e58e-bd74-4dfc-a25b-394de8399254" />
## `RouteMapTexture`
This tells the game what Minimap texture to load

<img width="475" height="30" alt="imagen" src="https://github.com/user-attachments/assets/2bb2ec64-8e60-4661-b4ed-3f826fb15706" />

## `SubLevelIndicesToUse`
For tracks that are always the same, just changing walls around in their layouts (like Cid's, Balamb and Midgar), this property is used to tell the game which track layout to load.

## `TrackingPoints` (wip)
Array containing a couple hundred 3D coordinate sets that each make up 3 lines through the track: one to tell the game where the middle is, where the right is, and where the left is. Every `TrackingPoint` must dictate which is the next `TrackingPoint` and which is the previous one, as well as the distance between them. They also have a property named `UpVector` which I believe to be how slanted it is (like how in Choco Hyperspeed you have a ramp that goes upwards and a path that goes downwards)
## `Checkpoints` (wip)
Track's checkpoints. a track only has 3 checkpoints (except Midgar having 2), 1 being reserved for the finish line.
Every checkpoint has 2 bools, designating if that checkpoint is either the start or the end. For all tracks in CGP, the first checkpoint is the finish line, which counts both as the start and the finish. While you could hypothetically make a Mario Kart World Intermission style track, the game still expects there to be 3 laps, and there is no known way of changing this, so... 
## `GridPoints`
The starting position for the players. Every track has 12 `GridPoints`, the first 8 being used for the 8 racers, and the last 4 being zeroed out. Every `GridPoint` has a position and a rotation value, which is where the player in that `GridPoint` spawns.
## `ItemPoints`
Array listing the amount of, type of, and position & rotation data of the item boxes in the track (crystals count as item boxes as far as the game is concerned). Each `ItemPoint` has two subproperties, `Lotteries` and `Transforms`. Each `Lottery` has two values, one of the kind of Item Box it is (Crystal, Copper, Silver or Gold), and another one for how many of that kind are in the item row. Every type of Item Box requires a separate `Lottery` entry, for example needing 4 entries for an item row made up of Copper, Silver and Gold eggs, in addition to Crystals (seen in Choco Farm Hyperspeed):

<img width="157" height="140" alt="imagen" src="https://github.com/user-attachments/assets/f5b7acaf-d58e-4365-8556-946e2ab4d78b" />

Each `ItemPoint` also has a `Transforms` array, one for each Item Box. Using the previous image as an example, we can see it has 4 entries, those being the following:


<img width="481" height="52" alt="imagen" src="https://github.com/user-attachments/assets/5588774b-b6cd-42cf-9817-747abf3894cf" /><img width="494" height="55" alt="imagen" src="https://github.com/user-attachments/assets/6a7480c5-1a30-4a09-a59e-d9df98b4aca1" /><img width="494" height="55" alt="imagen" src="https://github.com/user-attachments/assets/af25ed08-8c70-4851-8661-d37828954096" /><img width="501" height="56" alt="imagen" src="https://github.com/user-attachments/assets/8a39aff5-a949-47a7-b95b-80572d1b458a" />

You can see how the `ItemPoint` declares there are two Crystals in the item row, therefore there are 5 Item Boxes in this row. You then use `Transforms` to give each one of those positional, rotational, and scaling data (though the scaling data appears to be unused), and the game will then randomly shuffle the Item Boxes into those positions every race.

## `CourseShellPoints` (wip)
Plain and simple, this is where the game stores the "hitbox" position of boost pads and trick ramps (which are disconnected from their visual models).
It's an array made of `CourseShellPoints` (thanks squeenix), which themselves are arrays containing the position and rotation data for the boost pad/trick ramp, its size, and two other properties not yet understood: `StaticMeshCollision`, which is always set to `NoCollision`, and `StaticMeshOffset`, which stores usually zeroed out positional & rotational data, & 3d scale data.

Each `CourseShellPoint` also stores whether it's a boost pad or a trick ramp:

<img width="704" height="28" alt="imagen" src="https://github.com/user-attachments/assets/41c6e217-e1e2-43e8-b9d3-24e4ab68706e" />

## `RespawnPoints` (wip)

why the fuck do these exist

## `DeadzonePoints` (wip)

out of bound collision bubbles

## `BranchProbabilities` (wip)

(wip)

## `RouteMapPoints`

Array made up of 2d positions ranging from 0 to 1 in both axes, which the game then uses to place your character icon on the Minimap. Note that the Minimap's texture is merely cosmetic (except if you're the Jailbird bomb, what the fuck) and changing it won't change the character icon's position any.
There are exacly as many `RouteMapPoints` as there are `TrackingPoints`, since the game seems to use the latter to know where to place your character icon on the Minimap relative to the former

Contrary to `TrackingPoints`, `RouteMapPoints` don't need to specify who's up next in line and the distance between them, since they're 2d coordinates purely for the Minimap and isolated from the race otherwise

<img width="175" height="63" alt="imagen" src="https://github.com/user-attachments/assets/077f6660-67cd-4cd0-83fb-60934fdf5966" />

## `MagiciteLotteries` (wip)

I have no clue what the fuck this is, it just lists a bunch of magicite and some "start" and "end" numbers with it

Might dictate what magicite any given item box set can give? Unsure if that's a thing or not, though (how would this even work with custom magicite?)

### -End of Track Data File Structure-

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
