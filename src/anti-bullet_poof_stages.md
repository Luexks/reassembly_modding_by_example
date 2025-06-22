# Anti-Bullet Poof Stages
This chapter covers how to create fragments that do not produce (or minimize) [PSPs](./anti-bullet_poof_stages.md#anti-primary-spawn-poof-anti-psp-stages), [SPs](./anti-bullet_poof_stages.md#anti-spawn-poof-anti-sp-stages), and [DPs](./anti-bullet_poof_stages.md#anti-despawn-poof-anti-dp-stages).

There is included an [example of a clean fragment transition]
## Anti-Primary Spawn Poof (Anti-PSP Stages)
There is no known way to fully get rid of a PSP, only to make them as invisible as possible and to prevent them from overlapping to reduce the accumulation of noticable opaqueness.
```lua
{ 17000
	features=CANNON
    cannon={
    -- Anti-PSP stage:
        roundsPerSec=0.3
        power=10
		
        damage=50
        muzzleVel=200
        range=    200*1.2
		color=0xFFFF0000
		fragment={
    -- Genuine projectile stage:
			damage=50
			muzzleVel=1
			range=    1*1.2
			color=0xFF0000FF
			explosive=FRAG_NOFLASH
		}
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_anti-psp.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Anti-Spawn Poof (Anti-SP Stages)
Spawn poofs of non-primary stages are simple to remove using `explosive=FRAG_NOFLASH` on the stage which spawns the SP.
```lua
{ 17000
	features=CANNON
    cannon={
    -- Red, other primary stage.
        roundsPerSec=0.3
        power=10
        damage=50
        muzzleVel=200
        range=    200*1.2
		color=0xFFFF0000
		fragment={
    -- Blue, non-primary anti-SP stage:
			damage=50
			muzzleVel=1
			range=    1*1.2
			color=0xFF0000FF
			explosive=FRAG_NOFLASH -- Makes this stage anti-SP.
		}
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_anti-sp.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Anti-Despawn Poof (Anti-DP Stages)
Getting rid of despawn poofs is less simple than for spawn poofs. DPs can either be removed by:
1. Declaring `explosive=FINAL` on the stage which spawns the DP with the side effect that the bullet cannot to deal damage.
2. Declaring `explosive=FINAL` and `explodeRadius=1` on the stage with the side effect that the bullet always plays the explosion sound effect on despawn.
### Case 1: `explosive=FINAL`
Only having `explosive=FINAL` with no definition of `explodeRadius` makes the bullet use the default `explodeRadius` of zero, making it never hit anything and play no sound.
```lua
{ 17000
	features=CANNON
    cannon={
        damage=50
        roundsPerSec=1
        power=10
        muzzleVel=300
        range=200
		color=0xFFFFFFFF
		explosive=FINAL -- Makes this stage anti-DP.
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_anti-dp_1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Case 2: `explosvie=FINAL` and `explodeRadius=1`
Having `explosive=FINAL` and defining `explodeRadius=1` makes the bullet able to deal damage and makes it play the explosion sound effect on despawn.
```lua
{ 17000
	features=CANNON
    cannon={
        damage=50
        roundsPerSec=1
        power=10
        muzzleVel=300
        range=200
		color=0xFFFFFFFF
        -- Makes this stage anti-DP:
		explosive=FINAL
		explodeRadius=1
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_anti_dp_2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Example of a Clean Fragment Transition
The following fragment transition from the red bullet to the blue bullet contains no poofs, whereby the red anti-DP stage leads into the blue anti-SP stage:
```lua
{ 17000
	features=CANNON
    cannon={
    -- Red anti-DP stage:
        damage=25
        muzzleVel=200
        range=    200
        roundsPerSec=0.8
        power=10
		color=0xFFFF0000
		explosive=FINAL
		projectileSize=1
		fragment={
    -- Blue anti-SP stage:
			damage=25
			muzzleVel=1
			range=    1
			color=0xFF0000FF
			explosive=FRAG_NOFLASH
		}
    }
}
```
<video height=256 controls>
  <source src="diagrams/frag_clean_transition.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Note that despite this stage contains 50 units worth of damage, it can only ever deal 25 units of damage as the first stage's explosion will never overlap with anything as it's undefined `explodeRadius` is by default set to zero: