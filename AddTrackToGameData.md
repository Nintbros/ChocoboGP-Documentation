# Adding a Custom Track to the game files

Once you have your custom track at the ready with its track data UASSET file ready, you'll probably want to get that its own spot in Track Select instead of having to replace a track, no?

Here's how:

# Step 1

Open the finished UASSET file with uassetGUI and save it as a JSON file

# Step 2

Open the JSON file and add `U_CourseDataXYZ` to the NameMap

<img width="457" height="151" alt="imagen" src="https://github.com/user-attachments/assets/39842cf2-34d3-4266-a86d-01cbd2428543" />

(^this thing)

Like so:

<img width="218" height="276" alt="imagen" src="https://github.com/user-attachments/assets/b97b68bf-de1f-40ec-b728-0b15ee61ae9b" />

# Step 3

Scroll down to the very bottom of the file and find `ObjectName`. Replace it with your desired track ID (the XYZ):

<img width="421" height="130" alt="imagen" src="https://github.com/user-attachments/assets/5289c347-3410-4d0e-8663-fa176a607d01" />

# Step 4

Open the JSON with uassetGUI and save as an UASSET once again, then pack up the mod and enjoy
