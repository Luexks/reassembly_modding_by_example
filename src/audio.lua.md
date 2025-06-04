# audio.lua

`audio.lua` handles sound effects in Reassembly. The main use of it in modding is to give weapons or other blocks custom sound effects to make them sound cooler.

Audacity is a great tool for editing audio and is recomended for creating sounds for Reassembly. It can be downloaded at <https://www.audacityteam.org/download/>

Custom audio should be stored in the `<your mod here>/audio/` folder, which must be created manually. `audio.lua` locates samples using paths starting in the `audio/` folder. You can add subfolders to organise your sounds, but it is not necessary for most mods since different names for different sounds is usually good enough.

Audio files must be in the `.ogg` format (<https://fileinfo.com/extension/ogg>). If a sound is emitted from something in Reassembly's world, such as from a cannon as opposed to a GUI button, then it must be a single audio track, or mono sound file: that means that there is only one audio channel in the file. If you have a stereo (two channel) sound, then go to [here](./mixing_a_stereo_file_down_to_mono.md)

Unlike the other `.lua` files, `audio.lua` requires a large block of code at the top of the file, remember to copy and paste it:

```lua
-- Press Control-r in game to reload this file (when kEnableDevBindings = true)
-- all paths are relative to "data/audio/"


-- default event settings
{
   -- samples  = { { file1, file2 }, { file3, file4} }
   -- pick between file1 and file2, and between file3 and file4
   -- play both selected samples when event is triggered
   
   volume         = 1,          -- volume to play samples at (0 is silent)
   pitch          = 1,          -- pitch samples up and down
   pitchRandomize = 0.0,        -- increase or decrease pitch randomly by up to this amount

   rolloff        = 0.8,        -- 3d: how fast the sound attenuates
   minDist        = 100,        -- 3d: point it starts attenuating
   maxDist        = 9999999999, -- 3d: stops attenuating
   
   priority       = 0,          -- lower priorities will skip playback if there are too many sounds
   
   flags          = 0           -- special flags to control playback, connected with "|"
   --  stream:      load files while playing (set this for music tracks). No Polyphony
   --  music:       only play one music track at a time (with crossfading)
   --  loop:        loop event when finished playing
   --  round_robin: cycle through samples instead of picking randomly
   --  crosssync:   keep music offset when changing tracks
   --  cluster:     group event together with spacially nearby events and only play once
   --  cull_vol:    don't play event if volume <kSoundVolumeCull
   --  cull3d_vol:  don't start playing if calculated 3d vol is < kSound3DVolumeCull
}

-- settings for each event
-- event names ('e.g' ButtonPress) are hard coded in the game binary. 
```

Assume that the code block above is included in other examples of `audio.lua`.

Below is the syntax of the part of the `audio.lua` that you would actually code:

```lua
{
MyNewSoundEffect={
    samples={
        "MyNewSoundEffect_000.ogg"
        "MyNewSoundEffect_001.ogg"
        "MyNewSoundEffect_002.ogg"
    }
    flags=cluster|cull_vol|cull3d_vol
    priority=-2
    pitch=1.0
    minDist=120
    volume=0.75
    pitchRandomize=0.05
}
AnotherSoundEffect={
    samples={ "AnotherSoundEffect_000.ogg" }
    flags=cluster|cull_vol|cull3d_vol
    volume=0.5
    pitchRandomize=0.05
}
LaserSoundEffect={
    samples={ "LaserSoundEffect_000.ogg" }
    flags=cull_vol|cull3d_vol
    volume=0.3
}
}
```

In the `blocks.lua`, the `sound` field is used to define what sound a block plays when activated. The sound's name must be inside quote marks.

```lua
{ 17000
    features=CANNON
    sound="MyNewSoundEffect"
    cannon={
        -- Cannon fields here.
    }
}
```