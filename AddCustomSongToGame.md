wip cuz im lazy

# Prep work

Download [wavosaur](https://www.wavosaur.com), [AudioMog](https://github.com/Yoraiz0r/AudioMog/releases), and additionally [Audacity](https://www.audacityteam.org/) if wavosaur ends up having a bit of a bad UI for you (such as is the case for me)

Download desired song off the internet and open it up in Audacity/wavosaur, then figure out the loop points for the track (this is per-song, obviously)

For audacity in particular head to the timestamps at the bottom of the UI and set them to "samples", now note down the song loop's beginning (every loop has a beginning and an end) time in samples 

Then, note when the loop ends, and select and highlight everything past that and subsequently delete it

Once you have this down, amplify the FUCK out of the volume of the song then export as a .wav, and open it with wavosaur

Then press L (or Tools->Loop->Create Loop Points), then go to Tools->Loop->Properties

Input the noted down beginning time in samples into the "Start" box, then hit OK and save the file

Now extract the song you want to replace from the gamefiles (one day i'll figure out adding them without replacing)

Before proceeding, head to AudioMog's `TerminalSettings.json` config file, and replace its contents with this:

```json
{
  "TerminalSettings": {
    "ImmediatelyQuitOnceAllTasksAreDone": false,
    "LogLevel": 3
  },
  "ApplicationSettings": {
    "Parser": {
      "MusicFileFileVersion": {
        "Main": 2,
        "Sub": 1
      },
      "SoundFileFileVersion": {
        "Main": 2,
        "Sub": 1
      },
      "OverrideUAssetFileSizeOffsetFromEndOfFile": null
    },
    "AudioExtractor": {
      "ExtractAsRaw": false,
      "ExtractAsWav": true
    }
  }
}
```

Take the song's .uexp file (make sure its accompanying .uasset file is in the same folder) and drag it into AudioMog.exe

Head into the generated project folder and replace the .wav file in there with the one you just saved, then drag the JSON file found in there back into AudioMog, which should generate a brand new .uexp and .uasset files

Drag those into the accompanying mod folder and pack them up then apply the mod to enjoy your newly added custom song
