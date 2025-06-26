# Seeds

Compared to [root](./roots.md) blocks, seeds are more complicated in that they have many more interactions with other features. However, at its core, a `SEED` block can attach to an [environmental](./environmental_blocks.md) block, such as an asteroid, on collision and then grow into a blueprint. They can also be generated as [structures on asteroids](./structures_on_asteroids.md) in regions of their faction with structures enabled.

A basic seed has the `SEED` feature and a valid root shape, such as the [vanilla seed shapes](./vanilla_shapes.md#seeds):

```lua
{ 17000
    features=SEED
    shape=SEED_1
}
```

When it hits an asteroid, the seed will randomly select a blueprint that uses itself as the main seed. However, if the seed is launched from a preexisting plant, the child plant will use the same blueprint as the parent plant.

## Making plants

Create and save plants using the seed as you would any other modded ship. They should be in the `ships/` folder.

```
Reassembly/
└── mods/
    └── Faction 98/
        ├── ships/
        │   ├── 98_Seed_Structure_1.lua
        │   ├── 98_Seed_Structure_2.lua
        │   └── 98_Seed_Structure_3.lua
        ├── blocks.lua
        └── factions.lua
        └── regions.lua
```

Note that plants whose seed lacks the `COMMAND` feature will be saved to the `data/ships/` folder instead of in your mod's `ships/` folder with a name that suggests that they are of faction zero.

Move them to your mod's `ships/` and rename them to have the correct faction ID in their name (for example: `0_Plant.lua` -> `98_Plant.lua`).

```
Reassembly/
├── data/
├── └── ships/
│       └── 0_Plant_In_Wrong_Place.lua      <- Move this,
└── mods/
    └── Faction 98/
        └── ships/
            └── 98_Plant_In_Right_Place.lua <- to here.
```

## Seed Launchers

Seeds can be launched from [launchers](./launchers.md) and grow into plants on [environmental](./environmental_blocks.md) blocks. The value of the launcher's `replicateBlock` field must be set to the ID of the seed.

Note that the launcher must be defined after the seed.

```lua
{ 17000
    features=SEED
    shape=SEED_1
}
{ 17001
    features=LAUNCHER
    shape=RECT_LAUNCHER1
    replicateBlock=17000
    -- Other launcher fields here.
}
```

(You can also fully define the seed block inside the `replicateBlock` with an ID, e.g.: `replicateBlock={ 17001 features=SEED shape=SEED_1 }`, but it is not recommended since any plants that use the seed will corrupt if the launcher corrupts, and having the two block definitions seperate makes for cleaner code.)

## Plants that Grow Offspring Seeds

When a plant has a blueprint with extra seeds on it, the seeds are launched after being grown. In vanilla, this is how plants reproduce.

Note that the offspring seeds should be attached by their `ROOT` (yellow) port, otherwise the plant may spawn weirdly if generated in a sector on asteroids.

When the offspring seed hits an [`environmental`](./environmental_blocks.md), it will use the same blueprint as the parent plant.

Use `launchSpeed` to control how fast the offspring seed is ejected (different than `launcherSpeed` and `launchOutSpeed`).

```lua
{ 17000
    features=SEED
    shape=SEED_1
    launchSpeed=200
}
```

If plants that grow offspring seeds are spawned [on asteroids](./structures_on_asteroids.md) in a region, it is recommended to reduce asteroid density as the offspring seeds will all launch immediately, causing lag.

### `launchResources`

Defined in an offspring seed, `launchResources` is how much R a plant must store and spend to be able to launch the offspring seed after it has grown. When the offspring seed is launched, the `launchResources` value of R is subtracted from the parent plant.

Note that offspring seeds can still grow even if the `launchResources` value of R is not stored by the plant, the offspring seeds just cannot be launched.

```lua
-- The plant's R storage must be >= 50 to launch the offspring seed.
{ 17000
    features=SEED
    shape=SEED_1
    launchResources=50
}
```

## Lifetime of Seeds and Plants

(Seed and plant lifetimes are very janky.)

If you want a seed and its plant to last forever, then give it the field `seedLifetime=0`.

```lua
{ 17000
    features=SEED
    shape=SEED_1
    seedLifetime=0
}
```

Otherwise, unlike other blocks which use the [`lifetime`](./blocks_with_lifetimes.md) field, seeds use the `seedLifetime` and `launchLifetime` fields to control their lifetime and the lifetime of their plants.

Note that they do not work intuitively due to bugs; despite being used together in a seed's code in vanilla Reassembly, only one should actually be used. This is because `seedLifetime` overrides `launchLifetime`'s purpose.

 - Only `seedLifetime`: the lifetime of the seed is set to this when it is created and when it is planted on an [`environmental`](./environmental_blocks.md) block. This also determines the lifetime of blocks grown by the seed, even if the blocks have their own `lifetime`.
 - `launchLifetime`: controls the lifetime of the seed when it is launched. The lifetime of the seed when it is planted on an [`environmental`](./environmental_blocks.md) block is set to 60 seconds. Any blocks grown by the seed also have their lifetime set to 60 seconds.

Each time an [offspring seed](./seeds.md#plants-that-grow-offspring-seeds) finishes growing (not when launched), the lifetimes of all other blocks in the plant (including other offspring seeds, though this behaviour has little effect) are set to either `seedLifetime` seconds, if defined, otherwise to 60 seconds.

Because there is a difference to how seeds and their plants work depending on whether `seedLifetime` or `launchLifetime` is used, the use of one of the two fields must be decided on, although the choice is not very significant for normal seeds.

(Note that `seedLifetime` and `launchLifetime` are fields for the seeds and not the other blocks of the plant.)

```lua
{ 17000
    features=SEED
    shape=SEED_1
    seedLifetime=30
}

{ 17001
    features=SEED
    shape=SEED_1
    launchLifetime=30
}
```

## Plant Growth Cycles

Unlike other ships, plants wait until all of their currently growing blocks have finished growing before beginning the growth of all available blocks.

This causes plants to grow their blocks in a synchronised way, although it can be inconsistent, especially due to just launched offspring seeds being in the way of where they were grown.

## How Vanilla does Plants

As mentioned at the start of this chapter, seeds can have many interactions with different features, making them fairly complex. A good way to understand how to use seeds to create what you want is to understand how plants work in Reassembly.

Vanilla seed factors:
 - [`PHOTOSYNTH`](./resource_producers.md) with `photosynthPerSec` between 0.1 and 1.0.
 - [`THRUSTER`](./thrusters.md) with `thrusterForce=2000` and `launchSpeed=200` so that [offspring seeds](./seeds.md#plants-that-grow-offspring-seeds) can travel enough distance to collide with an asteroid.
 - [`elasticity=0`](./other_collision_bumper_and_elasticity.md#elasticity) to make seeds collide and attach to asteroids better.
 - `capacity=5` to store some R.

Vanilla plant factors:
 - Main seed at the base with an exposed `ROOT` port, offspring seeds at the end of stems attached to the stems with their `ROOT` ports.
 - Leaf blocks with [`PHOTOSYNTH`](./resource_producers.md) to generate R.
 - Leaf blocks have `capacity=100` so that the main seed can release more R on death if it has grown more leaves.
 - No [`FREERES`](./other_features_and_fields.md#commands-that-do-not-give-resources-on-death) on any block so that each block of the plant turns into its own R packet on death.

 ```lua
{ 17000 name="Seed"
    features=NOPALETTE|SEED|PHOTOSYNTH|THRUSTER
    shape=SEED_1

    launchLife

    photosynthPerSec=0.5

    thrusterForce=2000

    capacity=5

    launchSpeed=200
}
{ 17001 name="Stem"
    features=NOPALETTE
    shape=GEM_2
}
{ 17002 name="Leaf"
    features=NOPALETTE|PHOTOSYNTH
    shape=GEM_2

    photosynthPerSec=2.0

    capacity=100
}
{ 17003 name="Plant Launcher"
	features=PALETTE|LAUNCHER
	shape=RECT_LAUNCHER1
	
	replicateBlock=17000
	
    replicateTime=1
    launcherPower=100
    launcherOutSpeed=100
}
```
