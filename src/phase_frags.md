# Phase Frags

When a frag has enough stages with a high enough velocity it can phase through enemy ships, hence the name 'phase frag'.

Key factors:

 - High velocity of fragments, usually above 2000. (Can be inherited from previous stages.)
 - Short range per fragment. (Each fragment should only exist for a few frames.)
 - Many fragment stages.

Their behaviour changes depending on whether they have [`pattern=ABSOLUTE`](./fragments.md#absolute).

Two videos are included for each example:
 - Against a brick of target blocks with 50 health each in front of a hexagonal asteroid.
 - Against a scale 3 (the largest) Farmer shield at a slight offset so that the phase frag does not hit the shield head on (i.e.: not perpendicular to the tangent of the shield's collision circle).

The position of the weapon block is identical in each test.

## Without `pattern=ABSOLUTE`

Each stage increases `muzzleVel`, so it accelerates. The frag's angle can be diverted by hull and shields.

```lua
{ 17000
 	features=CANNON
	cannon={   damage=50 muzzleVel=2000 range=1 color=0xFFFFFFFF recoil=0 roundsPerSec=1
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	fragment={ damage=50 muzzleVel=  15 range=1 color=0xFFFFFFFF
	}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/phase_frag_without_pattern=absolute_hull.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<video height=256 controls>
  <source src="diagrams/phase_frag_without_pattern=absolute_shield.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Oscillating and Without `pattern=ABSOLUTE`

This frag oscillates between positive and negative `muzzleVel`, so it does not change velocity on its own. The frag's angle can be diverted by hull and shields.

```lua
{ 17000
 	features=CANNON
	cannon={   damage=50 muzzleVel=2000 range= 1 color=0xFFFFFFFF spread=0 recoil=0 roundsPerSec=1
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel= -15 range=-1 color=0xFFFFFFFF spread=0
	fragment={ damage=50 muzzleVel=  15 range= 1 color=0xFFFFFFFF spread=0
	}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/phase_frag_oscillating_without_pattern=absolute_hull.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<video height=256 controls>
  <source src="diagrams/phase_frag_oscillating_without_pattern=absolute_shield.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


## With `pattern=ABSOLUTE`

This frag stays at a constant speed of 2000 units per second. The frag's angle is not diverted by hull and shields.

```lua
{ 17000
 	features=CANNON
	cannon={   damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE recoil=0 roundsPerSec=1
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	fragment={ damage=50 muzzleVel=2000 range=2000/15 color=0xFFFFFFFF pattern=ABSOLUTE
	}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}
}
```

<video height=256 controls>
  <source src="diagrams/phase_frag_with_pattern=absolute_hull.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<video height=256 controls>
  <source src="diagrams/phase_frag_with_pattern=absolute_shield.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
