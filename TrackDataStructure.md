# Track Data File Structure
This documents how a track's internal data file is laid out.
Properties marked with an asterisk (*) are optional and not needed in every track file.

## `Level`
This property dictates which track model & collision gets loaded
<img width="750" height="31" alt="imagen" src="https://github.com/user-attachments/assets/9439f4e5-4398-46e2-b58a-2ada3e3e3565" />
## `IntroductionDemo`
This tells the game which camera sequence file to pair alongside the track, for the pre-race cutscene
<img width="656" height="25" alt="imagen" src="https://github.com/user-attachments/assets/97f8e58e-bd74-4dfc-a25b-394de8399254" />
## `RouteMapTexture`
This tells the game what Minimap texture to load

<img width="475" height="30" alt="imagen" src="https://github.com/user-attachments/assets/2bb2ec64-8e60-4661-b4ed-3f826fb15706" />

## `PlayBgmKey`*
String denoting the default BGM to use for the track.

For some god forsaken reason, Chocobo Farm doesn't have this property set, yet the game still loads its song properly, so maybe Bluegrass de Chocobo is the default track song if not specified.

## `SubLevelIndicesToUse`*
For tracks that are always the same and only have 1 collision model, just changing walls around in their layouts (like Cid's, Balamb and Midgar), this property is used to tell the game which track layout (aka which sets of walls amongst others) to load.

This parameter is optional and only needed if the track has a single collision file for all its layouts, as opposed to having a separate model per-layout.

## `TrackingPoints` (wip)
Array containing a couple hundred 3D coordinate sets that each make up 3 lines through the track: one to tell the game where the middle is, where the right is, and where the left is. Every `TrackingPoint` must dictate which is the next `TrackingPoint` and which is the previous one, as well as the distance between them. They also have a property named `UpVector` which dictates the current "gravity" for the current TrackingPoint. Yes, the funny chicken race has MK8 anti gravity support coded into it. Unfortunately rapid flips in gravity seem to "lock" the karts to a certain gravity value, so custom tracks can't get too crazy with it. Should work fine otherwise however.

Every TrackingPoint also *somehow* stores an "angle" for stuff like Swap (and by extension Odin Ult) to spit you out in. I have no clue how. It's driving me insane.

Reversing the order of these points in the physical array rather than just changing their Next & Prev pointers makes the game _very_ unhapy and leads it to crashing when loading a track.

(Note that this might be an unrelated side effect of how I am currently mass modifying track data)
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

## `SafezonePoints`* (wip)

every passing day i understand this game less and less

## `RespawnPoints`* (wip)

why the fuck do these exist. what the fuck do they do.

## `DeadzonePoints`* (wip)

seemingly out of bound collision bubbles, which is weird because you seem to be able to void out perfectly fine in tracks without these

## `BranchProbabilities`* (wip)

some stuff telling the cpu pathing (bahamut, camilla rings, choco/pa/ben/asura/raffa etc ults and similars included) which way is like the "default" path

they seem to be based on rng (though most are set to 100% chance) and have head and tail index data pointing to the specific TrackingPoints that make the beginning and end of that branched path

## `RouteMapPoints`

Array made up of 2d positions ranging from 0 to 1 in both axes, which the game then uses to place your character icon on the Minimap. Note that the Minimap's texture is merely cosmetic (except if you're the Jailbird bomb, what the fuck) and changing it won't change the character icon's position any.
There are exacly as many `RouteMapPoints` as there are `TrackingPoints`, since the game seems to use the latter to know where to place your character icon on the Minimap relative to the former

Contrary to `TrackingPoints`, `RouteMapPoints` don't need to specify who's up next in line and the distance between them, since they're 2d coordinates purely for the Minimap (and they reference the TrackingPoints for knowing where you are anyway) and isolated from the race otherwise

<img width="175" height="63" alt="imagen" src="https://github.com/user-attachments/assets/077f6660-67cd-4cd0-83fb-60934fdf5966" />

## `MagiciteLotteries` (wip)

I have no clue what the fuck this is, it just lists a bunch of magicite and some "start" and "end" numbers with it

Might dictate what magicite any given item box set can give? Unsure if that's a thing or not, though (how would this even work with custom magicite?)
