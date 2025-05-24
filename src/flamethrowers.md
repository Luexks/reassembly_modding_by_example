# Flamethrowers

Flamethrowers are a common weapon type that can be made in multiple different ways. However, this chapter contains one flamethrower (as well as a [version without `pattern=ABSOLUTE`](./flamethrowers.md#version-without-patternabsolute)) that can be modified to act differently.

The following flamethrower is designed to look similar to a real world flamethrower, which starts off yellow before going from orange to red and then fading out, while having a bright white center. The first three stages have been tailored specific `spread` values to achieve a specific, continuously morphing effect.

The purposes of the stages are as follows:
1. Primary, invisible stage with `spread=0.2` to make denser clusters of projectiles in the 2nd stage, as it has `roundsPerBurst=16`.
 - Predominantly cosmetic stages:
 
    2. This stage bursts into multiple fragments with `roundsPerBurst=16` across a spread of 0.1 radians. This is the only stage that uses `rangeStdDev` as it makes the following groups of bullets more clustered together.
    3. Similar to stage 2, but with a lower `roundsPerBurst` of 2 and with a higher alpha value to keep a consistent brightness by accounting for the bullets being more spread out.
    4. A dimmer stage that begins fading out the fragment and neither adds new bullets nor changes the angle.
    5. Still fading out.
6. Invisible, damage dealing stage.

```lua
{ 17000
    features=CANNON
    -- 1st stage:
	cannon={   damage=1 muzzleVel=  1 range= 0                color=1          spread=0.2 explosive=FINAL              pattern=ABSOLUTE                                    recoil=0 roundsPerSec=15
	-- Predominantly cosmetic stages:
        -- 2nd stage:
	fragment={ damage=1 muzzleVel=200 range=50 rangeStdDev=25 color=0x10FF7000 spread=0.1 explosive=FINAL|FRAG_NOFLASH pattern=ABSOLUTE projectileSize=2 roundsPerBurst=16
        -- 3rd stage:
	fragment={ damage=1 muzzleVel=100 range=25                color=0x20FF4000 spread=0.1 explosive=FINAL|FRAG_NOFLASH pattern=ABSOLUTE projectileSize=2 roundsPerBurst=2
        -- 4nd stage:
	fragment={ damage=1 muzzleVel=100 range=15                color=0x10FF2000            explosive=FINAL|FRAG_NOFLASH pattern=ABSOLUTE projectileSize=2
        -- 5th stage:
	fragment={ damage=1 muzzleVel=100 range=15                color=0x05FF2000            explosive=FINAL|FRAG_NOFLASH pattern=ABSOLUTE projectileSize=1
	-- 6th, damage dealing stage:
	fragment={ damage=5 muzzleVel=  1 range= 0                color=1                     explosive=      FRAG_NOFLASH pattern=ABSOLUTE
	}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/flamethrower.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Version Without `pattern=ABSOLUTE`

This is the same flamethrower, but it is more complex in that it does not use `pattern=ABSOLUTE`. This makes it fit in better with Reassembly's other weapons by allowing the flamethrower to inherrit the velocity of its ship.

Instead of using [`ABSOLUTE`](./fragments.md#absolute) to get rid of every stage's inherrited velocity, each stage with significant velocity is followed by a stage that cancels out the velocity, and then another that reverses the direction of the fragment.

```lua
{ 17000
 	features=CANNON|PALETTE
	-- 1st stage:
	cannon={   damage=1 muzzleVel=   1 range= 0                color=1          spread=0.2 explosive=FINAL                                                  recoil=0 roundsPerSec=15
	-- Primarily cosmetic stages:
        -- 2nd stage:
	fragment={ damage=1 muzzleVel= 200 range=50 rangeStdDev=25 color=0x10FF7000 spread=0.1 explosive=FINAL|FRAG_NOFLASH projectileSize=2 roundsPerBurst=16
	fragment={ damage=1 muzzleVel=-200 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=1 muzzleVel=  -1 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
        -- 3rd stage:
	fragment={ damage=1 muzzleVel= 100 range=25                color=0x20FF4000 spread=0.1 explosive=FINAL|FRAG_NOFLASH projectileSize=2 roundsPerBurst=2
	fragment={ damage=1 muzzleVel=-100 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=1 muzzleVel=  -1 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
        -- 4nd stage:
	fragment={ damage=1 muzzleVel= 100 range=15                color=0x10FF2000            explosive=FINAL|FRAG_NOFLASH projectileSize=2
	fragment={ damage=1 muzzleVel=-100 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=1 muzzleVel=  -1 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
        -- 5th stage:
	fragment={ damage=1 muzzleVel= 100 range=15                color=0x05FF2000            explosive=FINAL|FRAG_NOFLASH projectileSize=1
	fragment={ damage=1 muzzleVel=-100 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
	fragment={ damage=1 muzzleVel=  -1 range= 0                color=1                     explosive=FINAL|FRAG_NOFLASH
	-- 6th, damage dealing stage:
	fragment={ damage=5 muzzleVel=   1 range= 0                color=1                     explosive=      FRAG_NOFLASH
	}}}}}}}}}}}}}}
}
```

The example video shows how the version of the weapon without `ABSOLUTE` inherits the velocity of the ship its on, and how it aids in ranged combat.

<video height=256 controls>
  <source src="diagrams/flamethrower_no_absolute.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
