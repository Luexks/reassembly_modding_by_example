# Fragments
When a bullet is destroyed, it can produce fragments. These fragments can also produce fragments when they are destroyed, creating one of the most versatile systems in Reassembly modding.

Fragments are nested within projectile code and have the same field types as base cannons except for those which wouldn't make sense.

Look at the code below and look at the similarities between the base cannon bullet and the fragment which is nested within it:
```lua
{ 17000
    features=CANNON
    cannon={
        damage=100
        roundsPerSec=5
        muzzleVel=1000
        range=1000
        power=10
        spread=0.1
        color=0xFFFFFFFF
        recoil=1

        burstyness=1
        roundsPerBurst=5

        explosive=ENABLED
        explodeRadius=50

        fragment={
            damage=50
            -- Fragments don't have `roundsPerSec`.
            muzzleVel=500
            range=500
            -- Fragments don't need `power`.
            spread=0.1
            color=0xFFFFFFFF
            -- Fragments have no need to exert `recoil`.

            -- Fragments also don't have `burstyness`.
            roundsPerBurst=5

            explosive=ENABLED
            explodeRadius=25
        }
    }
}
```
In fragments, `roundsPerBurst` is repurposed as the amount of fragments released when a bullet is destroyed.

In the code extract above, the base cannon bullet will split into 5 fragments, which are all identical. The fragments will also be created at a spread of 0.1 radians, or ~5.72°, as defined by the fragment's `spread` field.

<video  controls>
  <source src="diagrams/fragment_first_example.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Fragment Chaining
As fragments can be nested within each other, we can create fragment chains. Below is an example of one using conventional one-line fragments for easy reading:
```lua
{ 17000
    features=CANNON
    cannon={
        damage=100
        roundsPerSec=1
        muzzleVel=50
        range=50
        power=10
        -- Some fields have been left out for ease of explaining.

        fragment={ damage=100 muzzleVel=50 range=50 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=50 range=50 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=50 range=50 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=50 range=50 roundsPerBurst=1
        }}}} -- Closing brackets are lined up at the end of the chain.
    }
}
```
In this code extract, there will be 5 fragment projectiles that spawn after one another in a chain.

## The Relationship of `range` and `muzzleVel`
If you fire the cannon from the code extract above, you might notice something unexpected if you are unfamilier with fragment modding. Each new fragment is faster than the last by 50 units per second:

<video  controls>
  <source src="diagrams/fragment_chain_speeding_up.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

This is caused by each successive fragment inheriting the sum of the velocities of all the bullets that came before it.
To have uniform velocities on the bullets, one might expect the solution to be to make the `muzzleVel` equal 0, but this does not work:
<video  controls>
  <source src="diagrams/fragment_chain_going_on.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

```lua
    cannon={
        damage=100
        roundsPerSec=1
        muzzleVel=50
        range=50
        power=10

        fragment={ damage=100 muzzleVel=0 range=50 roundsPerBurst=1
        -- None of the other fragments are reached.
        fragment={ damage=100 muzzleVel=0 range=50 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=0 range=50 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=0 range=50 roundsPerBurst=1
        }}}}
    }
```
Although the second bullet has velocity, it is inherited from the first stage. Think back to how bullet duration is calculated based on only a bullet's `muzzleVel` and `range`, not its current velocity.

Now, understand that the second bullet will never transition to the third stage as the second bullet is "attempting" to travel a `range` of 50 at a `muzzleVel` of 0. The journey to travel 50 units at 0 units per second is uncompletable, the bullet will never enter the third stage.

To achieve uniform velocities, we must make the `muzzleVel` unnoticably small as well setting its `range` small enough that the fragments' duration is calculated to not be infinite. 

If we want the fragments to last for one second, similar to the base bullet, then we can set `range` to 1 and the `muzzleVel` to 1. The bullet will travel 1 unit at 1 unit per second over a time of 1 second.

<video  controls>
  <source src="diagrams/fragment_chain_uniform_velocity.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

```lua
    cannon={
        damage=100
        roundsPerSec=1
        muzzleVel=50
        range=50
        power=10

        fragment={ damage=100 muzzleVel=1 range=1 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=1 range=1 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=1 range=1 roundsPerBurst=1
        fragment={ damage=100 muzzleVel=1 range=1 roundsPerBurst=1
		-- All fragments occur. success!
        }}}}
    }
```
Strangely, a bullet trying to travel a `range` of 0 at a `muzzleVel` of 0 completes its journey.
## Patterns
For more control over how bullets are spawned, you can select various pattern flags for the `pattern` field of a bullet. They can be used in both base bullets and fragments. 

Below is an example of a cannon using the `RANDOM` pattern, which would be the same as having `pattern` not defined.
```lua
    cannon={
        damage=100
        roundsPerSec=1
        muzzleVel=50
        range=50
        power=10
        recoil=0

        spread=pi*2
        pattern=RANDOM
    }
```
Below are all the bullet patterns, they can all be used on both base cannon bullets and fragments except for `WAVE`, which can only be used on base cannon bullets.
### Random
`pattern=RANDOM`: default spread behaviour, choosing a random angle in the specified spread.
```lua
	cannon={ spread=pi*2 pattern=RANDOM

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_random.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Constant
`pattern=CONSTANT`: bullet will angle exactly at the spread angle. Positive `spread` angles bullet counterclockwise while negative `spread` angles bullets clockwise.
 
 Firing counterclockwise:
 ```lua
	cannon={ spread=pi*0.5 pattern=CONSTANT

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_constant_positive.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Firing clockwise:
 ```lua
	cannon={ spread=pi*-0.5 pattern=CONSTANT

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_constant_negative.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Spiral
`pattern=SPIRAL`: bullets are evenly distributed within the spread angle. Needs `roundsPerBurst` and `burstyness` defined on base cannon bullets but only needs `roundsPerBurst` defined on fragments.
 ```lua
	cannon={ spread=pi*0.5 pattern=SPIRAL roundsPerBurst=5 burstyness=0.5

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_spiral.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Wave
`pattern=WAVE`: bullets are distributed according to a sine wave within the spread angle. Do not use on fragments.
 ```lua
	cannon={ spread=pi*0.5 pattern=WAVE roundsPerBurst=20 burstyness=0.5

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_wave.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Absolute
`pattern=ABSOLUTE`: bullets do not inherit velocity of ship or previous bullets. It can be mixed with any of the other pattern flags.

 This is without `ABSOLUTE`:
 ```lua
	cannon={ spread=0

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_absolute_no.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

 This is with `ABSOLUTE`:
 ```lua
	cannon={ spread=0 pattern=ABSOLUTE

        damage=100 roundsPerSec=5 muzzleVel=50 range=50 recoil=0 }
 ```
<video height=256 controls>
  <source src="diagrams/fragment_pattern_absolute_with.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

 ## Explosive Flags for Fragments
There are fragment specific alternatives for `ENABLED`, `FINAL`, and `PROXIMITY` for the `explosive field`. Respectively, they are:
 - `FRAG_IMPACT`: bullet fragments when hitting a target but not when the bullet reaches the end of its range.
 - `FRAG_FINAL`: bullet fragments at either the end of its range or when the bullet's damage output is exhausted.
 - `FRAG_PROXIMITY`: bullet fragments when within proximity of an attackable block.

There is also `FRAG_NOFLASH`, which makes bullets with this flag spawn without producing a frag spawn particle.

([Explosive flags for non-fragments](./cannons.md#explosive-cannons))