quick and dirty guide so i dont forget

files to modify:

>/Item/DT_Item - need to add item IDs for the new skins

>/Player/param/PlayerXXDataAsset - the 3 ride config files hold information on which mesh is tied to what skin

>/Player/param/DT_PlayerDatabase - the skinlist for the character on the engine (non-UI) side is defined in here

>/UI/Menu/CharacterSelect/Parts/DataTable/DT_UI_SkinList - the skinlist for the UI (no UI = can't select skin even if it exists)

>/UI/Common/CharacterData/CharaData/UI2D[CharaName] - config file for each individual character that also lists their skinlist

NOTE: Path is /UI/UPdate/Common/CharaData for DLC characters.

What specifically to change to every file:

DT_Item: We need to add the actual item ID of the skin to the game. Just leech off of any other skin the character already has, copy paste the entry, change the item ID to a valid one, and make sure to add it to the namemap. All the actual ID config should have been done by the entry you leeched off of.

PLayerXXDataAsset: At the root of the UAsset data, will be a list of the information. There will be a list of "CharaSkinMeshX" that link to a model path. You will want to add a new one with the respective number and path to the model. Note that there is a hardcoded maximum of 17 skins per character in the game. `CharaSkinMesh` is a hardcoded enum that we do not have access to and thus cannot add entries to. After CharaMesh16, the game stops recognizing them.

DT_UI_SkinList: Holds item IDs for each player ID. Just append yours to the respective guy.

UI2D[CharaName]: Inside the `IconCostume`, `IconCostumeSel`, and `TextCostumeSel` arrays, you must add the appropiate data for your skin. `IconCostume` holds the link to the icon texture of the skin. `IconCostumeSel` does the same but for the white outline around the skin. Yes, that is a separate image. `TextCostumeName` holds the string ID for the Skin's name.

IMPORTANT NOTE: Your custom meshes must use the common skeleton found in pl00, as well as the specific materials. For the most part, you can just see what other skins for that character do with their materials and skeleton, and just copy that.
