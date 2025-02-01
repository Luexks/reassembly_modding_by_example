# Mod Structure

Local (i.e., what you create) mod folders are stored in the `mods/` folder, which must be created next to the `data/` folder at the following location:
`C:/Users/<your username here>/Saved Games/Reassembly/`
You should now have what looks like this:
```
Reassembly/
├── data/
└── mods/           # This is the folder you just created
```
Now, make your new mod's folder into `mods/`.
```
Reassembly/
├── data/
└── mods/
    └── Terran V2/   # Name it something suitable.
                    # If it's a faction mod, call it the name of the faction.
```

There are multiple `data/` folders scattered around your computer. One in `Save Games/`, one in the games actual installation, and one in the Steam cloud folder if you're using that. Mod structure mirrors the structure of the Reassembly `data/` folders. If your mod has the same folder and file names as those in the Reassembly `data/` folders then it will work. The `data/` folders are grouped up when the game is run and all the common files and folders between both mods and the base game are merged.

This resource is organised by Reassembly's moddable files and folders.
Below is what mod folders tend to look like:
```
Reassembly/
├── data/
└── mods/
    └── Blue Sun/
        ├── audio/
        │   ├── sub_folder_for_lasers/
        │   │   ├── laser_0.ogg
        │   │   ├── laser_1.ogg
        │   │   └── laser_2.ogg
        │   ├── machine_gun_0.ogg
        │   ├── machine_gun_1.ogg
        │   └── machine_gun_2.ogg
        │
        ├── ships/
        │   ├── 256_ship_1.lua
        │   ├── 256_ship_2.lua
        │   └── 256_ship_3.lua
        │
        ├── folder_for_unused_ships_that_i'll_delete_before_i_post_the_mod/
        │   └── 256_ship_wip.lua
        │
        ├── audio.lua
        ├── blocks.lua
        ├── cvars.txt
        ├── factions.lua
        ├── regions.lua
        ├── shapes.lua
        │
        ├── preview.png         # Here's your reminder that all of these images individually must be >1 MB to get uploaded to the Steam Workshop.
        ├── capture1.jpg        # You can have as many `capture#.jpg`s as you want.
        ├── capture2.jpg
        ├── capture3.jpg
        │
        └── anything.txt        # Random stuff that won't be picked up by the game
```