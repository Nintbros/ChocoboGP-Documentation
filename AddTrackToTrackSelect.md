# Step 1
Extract both `UI/Menu/CourseSelect/DataTable/DT_UI_CourseSelect` and `Race/Data/DT_Location` as JSON files

# Step 2
Open `DT_Location` up in your text editor of choice, then navigate to the track you want to add buttons to (for example, by searching `ELocationId::CHOCOBOFARM` for Choco Farm)

# Step 3
Navigate to the `Value` array that contains track file data (e.g. `/Game/Course/Data/U_CourseData010.U_CourseData010` for Choco Farm Short)

# Step 4
Copy and paste the array (note that order matters), then change the track file to the corresponding track (change both numbers!)

# Step 5
Save changes & exit, then open `DT_UI_CourseSelect`

# Step 6
There are 3 properties the game cares about, and won't add a button to track select if they aren't there. Those are `CourseSize` (course select length indicator), `CourseNameMessageID` (what tells the game the name of the layout, e.g. Hyperspeed/Technical/Long etc), and `CourseMinimap`, which is the minimap icon for track select.

Leech off of previous entries in the track you wanna add more layouts to (like with `DT_Location`) and modify the values as needed

# Step 7
Save & exit, convert the JSON files back to UASSET, and pack them up into a mod
