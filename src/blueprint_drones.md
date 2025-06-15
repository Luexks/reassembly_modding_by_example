# Blueprint Drones

Blueprint drones are special drones that can grow blocks according to a specified ship blueprint.

Key/recommended factors:
 - Drone command block (must have its own ID). Requires [`COMMAND`](./commands.md), [`REGROWER`](./commands.html?highlight=regrower) or [`ASSEMBLER`](./commands.html?highlight=assembler) (depending on if you want it to rebuild using debris), and [`FREERES`](./other_features_and_fields.md#commands-that-do-not-give-resources-on-death); also needs [`lifetime`](./blocks_with_lifetimes.md).
 - Bespoke blocks (hull, thrusters, weapons) for the blueprint drone that have [`FREERES`](./other_features_and_fields.md#commands-that-do-not-give-resources-on-death), [`lifetime`](./blocks_with_lifetimes.md), and [`NOPALETTE`](./getting_blocks_to_show_up_in_the_campaigns_databank.html?highlight=nopalette). See [below](./blueprint_drones.md#bespoke-blocks-for-blueprint-drones) to see how to make these using [block extensions](./block_extensions.md).
 - (Optionally give the blocks [`NOCLIP_ALLY`](./noclipping_blocks.html?highlight=noclip_ally) just as with standard launchables.)
 - The blueprint drone's ship file in [`ships/`](./mod_structure.html?highlight=ships/).
 - In the drone command's `command={}` field, a declaration of `blueprint="<your blueprint drone name here>"`.
 - In the launcher block, set `replicateBlock=<ID of your drone command block here>`.

Alternative factors:
 - Bespoke blocks are not strictly necessary, standard faction blocks used on normal ships can also be used on blueprint drones, especially if standalone blocks with specific features for blueprint drones are not required.
 - [`lifetime`](./blocks_with_lifetimes.md) is not required if a blueprint drone with an indefinite lifetime is desired, which would make the launcher a pseudo-[factory](./factories.md) block.
 - [`EXPLODE`](./explosive_blocks.md) and its required fields can be used on a drone command block to make it explode instantly after its lifetime ends.
 - [`FREERES`](./other_features_and_fields.md#commands-that-do-not-give-resources-on-death) is not strictly required.

Build the blueprint drone in the same way as you would with any other ship with any bespoke blocks if you made them. Comment out (add `--` at the start of the line of) `lifetime` so that the blueprint drone does not despawn while building. Add it back after finishing. Use [`ssave` (`ss`)](./sandbox_basics.md#saving-modded-ships) and make sure that the blueprint is in `ships/`.

Below is an example of a blueprint drone and its dedicated blocks for faction 98:

```
Reassembly/
└── mods/
    └── Faction 98/
        ├── ships/
        │   └── 98_My_Blueprint_Drone.lua
        └── blocks.lua
```

```lua
-- blocks.lua

-- Dedicated Blueprint Drone Parts:
{ 17000
	features=NOPALETTE|FREERES
	group=98
	growRate=50
	lifetime=20
}
{ 17001
	features=NOPALETTE|FREERES|GENERATOR
	group=98
	shape=OCTAGON
	generatorCapacityPerSec=20
	powerCapacity=10
	capacity=0
	growRate=50
	lifetime=20
}
{ 17002
	features=NOPALETTE|FREERES|THRUSTER
	group=98
	shape=THRUSTER_RECT
	thrusterForce=1000
	thrusterColor=0x7FFF0000
	thrusterColor1=0x7FFFAA00
	growRate=50
	lifetime=20
}
{ 17003
	features=NOPALETTE|FREERES|LASER|TURRET
	group=98
	shape=OCTAGON
	turretSpeed=12
	laser={
		damage=50
		range=1000
		power=2
		color=0xFFFF5500
		width=2
		decay=0.1
	}
	growRate=50
	lifetime=20
}

-- Blueprint Drone Command:
{ 17004
	features=NOPALETTE|FREERES|COMMAND|REGROWER
	--features=NOPALETTE|ASSEMBLER|COMMAND|REGROWER
	group=98
	shape=COMMAND
	command={ blueprint="98_My_Blueprint_Drone" }
	lifetime=20
}

-- Launcher:
{ 17005
	features=PALETTE|LAUNCHER
	group=98
	shape=RECT_LAUNCHER1
	
	replicateBlock=17004
	
    replicateTime=1
    launcherPower=100
    launcherOutSpeed=100
}
```

<video height=256 controls>
  <source src="diagrams/blueprint_drone.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<video height=256 controls>
  <source src="diagrams/blueprint_drone_deconstructing.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Bespoke Blocks for Blueprint Drones

If you want a blueprint drone to use the same blocks that your faction normally uses but with different features, then you should use [block extensions](./block_extensions.md).

An example of this for a hull block and a laser is below:

```lua
-- Normal Faction Blocks:

{ 17000
	features=PALETTE
	group=98
}
{ 17001
	features=PALETTE|LASER|TURRET
	group=98
	shape=OCTAGON
	turretSpeed=12
	laser={
		damage=50
		range=1000
		power=2
		color=0xFFFF5500
		width=2
		decay=0.1
	}
}

-- Dedicated Blueprint Drone Blocks:

{ 17100 extends=17000 features=FREERES|NOPALETTE              growRate=50 lifetime=20 }
{ 17101 extends=17001 features=FREERES|NOPALETTE|LASER|TURRET growRate=50 lifetime=20 }
```